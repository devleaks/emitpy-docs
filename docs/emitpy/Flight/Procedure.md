Coded Instrument Flight Procedures are read from FAA data files and exposed as flight segments usable by Emitpy.

The following entities are created:

- Terminal (an airport)
- RWY (a runway, if available, two opposite runways are paired, like 34L and 16R)
- SID
- STAR
- APPCH

Also, available in the Airspace structure are
- Fixes
- Holding positions and patterns

For an airport involved in a flight, those procedures are loaded "on demand" ([[Airport#AirportWithProcedures]]). (I.e. all procedures are not loaded for all airports.)


# Turns

During the flight route smoothing, turns are modified to provide a realistic flight path. At each vertex, the flight proceeds with either a fly-by or a fly-over path, as requested by waypoints.
## Fly-By

For fly-by waypoints, a smooth standard turn is built in front of the waypoint. For very sharp angle turns, this can lead to very early turns.
A center of turn path is found between the two segments and then a turn is added, tangent to both segments.

![[flyby.png]]

## Fly-Over

Flight over waypoint proceed with two coordinated standard turns. After flying over the way point, the aircraft turns in the direction of the next way point. The turn angle is set to 150% of the original turn angle toward the next way point (but no more than a 180° U-turn) to allow the aircraft to fly back on next leg. From the new temporary heading, the aircraft proceed with a smooth fly-by at the intercept point to continue its journey towards the next waypoint.
This is done only if the aircraft has time to join the next leg smoothly before the reaching the next waypoint.

![[flyover.png]]

When waypoints are too close, some turns may not be performed fully. The fallback is a fly-by towards the next way point, which may, sometimes, lead the aircraft temporary out of its allowed airspace. In extreme circumstances, when waypoints are too close, some waypoint may be omitted or suppressed from the flight path.

Radius is computed at turn entry speed to complete a standard turn (360° in 2 minutes). Radius remains contant for the duration of the turn, even if aircraft speed changes during the turn. Aircraft will accelerate/decelerate at turn exit to comply with the next leg requirements.

When turn angle is too shallow, turn smoothing my be omitted.
