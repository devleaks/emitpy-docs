*About airspace restrictions and their partial handling.*

Emitpy is not a professional tool, but rather an accessory simulator that is used to generate realistic but imperfect flight paths. It has therefore the following limitations.

# Notes about Restriction Handling

To simplify restriction handling, Emitpy uses a naive algorithm that works as follow:

## Restrictions when Climbing

When climbing, we clear *above altitude* restrictions one after the other.
The rationale being that it is harder to climb to clear above altitude restrictions.
When climbing towards the next *above altitude* restriction, we remain under *below altitude* restrictions that may occur while reaching the next above altitude restriction, and reduce climb rate to respect those restrictions.

As now, change of vertical movement is solely done exactly *at* waypoints, not « between » waypoints. To optimise flight plans and movement, it would be advisable to revise this limitation and start climbs or descend at more appropriate times, taking into account finer aircraft performances and other preoccupations like fuel usage and environmental constraints. This process it complex and out of the scope of this simulator.

## Restrictions when Descending

When descending, we clear *below altitude* restrictions one after the other.
When descending towards the next *below altitude* restriction, we remain above *above altitude* restrictions and reduce descend rate to respect those restrictions. This sometimes requires expediting following descends to meet following restrictions.

## Top of Descend

The Top of Descend is searched backwards from the first below altitude restriction. The length of the first descend from cruise altitude is limited to ~100km (54Nm).

The static value is compared to the rule of thumb value

```
(3 x height) + (1nm per 10kts of speed loss) + (1nm per 10kts of Tailwind Component)
Notes:
10kts = 5.144444 m/s
Tailwind: add 10nm for safety
```

Both values are always very close for typical airliners descending to typical STAR.

If, for a short flight, the climb was not finished at the top of descend, a warning is issued and the flight level of the whole flight is adjusted accordingly. This should not happen if flight level was computed by Emitpy because Emitpy has a procedure to compute the optimum flight level for a given distance.

# Airway Restrictions

There is currently no airway restriction implemented, although all hooks to do it are ready. (One day, may be.)

The only constraint that are handled during flight plan calculation are airway *types* (high, low, or both) and *direction* (one way, two way). These restrictions are sometimes relaxed if no route can be found between two airports. In this cas, a warning is issued together with the restriction that is abandoned.

While left as a parameter, transition from low to high airways is always performed at FL180.

# Speed Restriction

Speed restriction is enforced last on the whole flight, one restriction at a time, taking into account flight phases (takeoff, climb, acceleration, cruise...)
THERE IS NO ADJUSTMENT of climb rates, distances, etc. if speed was modified because of a restriction. 
We understand this is a limitation, acceptable under most circumstances, the main reason being that resprictions have, themselves, been implemented taking into account aircraft performances (PBN).

While left as a parameter, restriction to maximum 250kn is enforced at FL100, unless a local constraint impose otherwise.

# Notes about Vertical Navigation

To easy vertical navigation, the following is imposed to all flight movements.

![[vnav.png]]

On take-off, the aircraft climbs in a straight line, aligned with the runway, at its nominal initial climb speed and vertical speed up to an altitude of **1500ft** (450m) ABG, which is tipically reached after 3 to 5km.
There is then a direct-to-fix vector to the first point of the SID, if any, or to the first point of the journey. The last point of *initial climb* is marked as such.
If there is no SID procedure, the aircraft climbs at its nominal speed and climb rate until it reaches the planned flight level.

On landing, there is an *artificial* final fix point placed at **2000ft** from the touch down point and the aircraft uses a **600ft/min** vertical speed. During that time, it flies at its landing speed.
On final approach, there is a direct vector from the last point of the approach procedure to this *artificial* final fix point. If the approach procedure terminates below 2000ft, the artificial fix point is moved towards the touch down point to intercept the last procedure altitude.
If no STAR and/or approach procedure is used, the artificial final fix behaves like the last at or below altitude restriction.

There is no environmental contraint. (CO2 reduction, fuel economy, noise abatment, etc. sorry.)