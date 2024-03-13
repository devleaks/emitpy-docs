#flight 
A Flight Route is a flight path from an origin airport to a destination airport only flying on airway segments.

# Notes on Route and Flight Plan Building

High and Low airways are not distinguished, they are all airways. (May be refined later, algorithm needed.)

QFU is determined on both departure and arrival airport if possible solely based on wind direction at the location, at the time of the flight if possible, using (historical) METAR and/or TAF. If several runways meet wind orientation restrictions, one is randomly selected.
If no wind direction is available at an airport, all runways can be used for take-off or landing.

There is no "local policy" enforcement, i.e. 25R for taking-off and 25L for landing.

When a runway has been selected, flight procedures are selected. Procedures that makes the shortest flight in distance are selected.

The above selection process makes a flight fairly random. Supplying the same parameters can lead to several flight plans and paths for the same departure and arrival airport. A pair of multi-runway large airports with no wind (i.e. random runway) can lead to up to a few dozen of different flight plans and paths for the same departing and arrival airports.

To circumvent this randomness, in case of need, to reproduce the exact same flight, it is optionally possible to supply runways and procedures to use at both ends. This leads to a repeating flight path, provided weather is not changed. This allow, for example, to test different aircrafts or variables with different performances for the same flight.

### Take-Off, Initial Climb and Final Fix

Take-off always occurs in a straight line, ascending at initial-climb speed and vertical speed, up to 1500ft. After that, there is a Direct Fix to the first point of the SID procedure if any.

On arrival, the last point of the approach procedure always leads (Direct to Fix) to an *artificial final fix* point that is always on the slope of a line that starts at 2000ft (ABG) and terminates 300m after the runway threshold, where kiss-landing always occurs. The slope of the line is adjusted for aircraft landing speed and a vertical speed of 600ft / minute.

On arrival also, if the last point of the flight plan does not contain an altitude restriction, it is assigned one. The altitude set for the restriction depends on the distance of this last point to the airport. (A speed restriction might also be applied.) Please recall that during descent, altitude restrictions are carried forward to the next point if he next point does not have a restriction.

### Transitions

Transitions are always Direct to Fix. To the next point.
This may result in sometimes in unusual turns from last procedure waypoint to next procedure waypoint.

![[transition.png]]
# About Taxiing

Taxi occurs on the local network of taxiways.

Currently, the following simplification have been taken into account:
- No one-way taxiway (they are all two-ways).
- Taxiway width not taken into account for aircraft class (width).
- Runways are most of the time taxiways. Therefore, the shortest path to a destination may result in a U-turn on the runway.
- Speed on taxiways is uniform.