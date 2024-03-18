A Flight is a container entity that represent the movement of an aircraft between two airports, one of them being the Managed Airport.
There are two types of Flight:
- Arrival flights are flights that arrive at the Managed Airport,
- Departure flights are flights that leave the Managed Airport.

The creation of a flight is a 3 step process:

- Creation of the Flight Plan
- Creation of the Flight Movement, including airport procedures and taxi at the managed airport
- Smoothing of the Flight Movement to make the journey more realistic.

## Flight Plan

A Flight Plan is a succession of flight segments.

First a **Flight Route** is created from departure airport to arrival airport. Route is created following high and low airways. An arbitrary flight level is decided based on the distance between the two airports.

The flight plan is completed by **flight procedures**, if available, around both terminal areas. Flight produces are selected according to weather information (QFU from weather METAR and/or TAF), and some randomness. Airport local usage and rules are not enforced, but rather randomly selected.

A flight plan only contains lateral navigation and restrictions.

Procedures are inserted and respected. Cruise is adjusted between end of SID and start of STAR; cruise points may be removed if they imply in-flight U-turns.

## Flight Movement

### Movement Complements

The Flight Movement is a [[Movement]]. It is the flight plan completed with:

1. Vertical navigation with altitude restrictions,
2. Lateral and vertical navigation with speed restrictions,
3. Taxi in or out at the managed airport, from the runway to the parking position for arrival flights, or from the parking position to the start of the runway for departing flights.

Vertical navigation is added taking into account Aircraft Performances for speeds, accelerations, and operating limits. Vertical navigation is geometric, taking into account aircraft capabilities.

Airway restrictions are not taken into account. Aircraft either flight high altitude airways, or low altitude airways, or both combined together. (One day aircraft will flight low airways below ~ FL180 and high airways above.)

#### Notes on Flight Movement

The relation between flight plan waypoints and movement points is preserved. However, several movement points may be attached to a single flight plan waypoint.

Mots natably, for example:

- Take off hold, take-off, and end-of-initial-climb points are all attached to the departing airport.
- (Artificial) final fix, touch-down, and end-of-roll are all attached to the arrival airport waypoint.
- When a "smooth turn" (fly by or fly over) is added at a fly plan waypoint, all movement points are attached to the flight plan waypoint.

### Flight Smoothing

At this stage, the flight consists of straight flight segments with no smooth transitions. The smoothing algorithm adds a few limited adjustment to the flight path (fly-by waypoints, smooth procedure turns, straightforward transitions (direct-to), etc.)

Finally, data and meta data is carried over from vertices to vertices, linearly interpolating values when necessary.

The Fliht Movement is a succession of segments, each vertex has information relative to the aircraft movement (speed, altitude, vertical speed, etc.)
## Summary
![[flight-movement.png]]
## Flight Times

Flights have three times associated with them:

- The Scheduled date/time is mandatory and always used to create the flight.
- If an Estimated time of arrival/departure is available, the flight can be "rescheduled" accordingly.
- Finally, when a flight is completed, an Actual flight time is recorded.

Scheduled and actual flight times cannot be changed.
If the Estimated time is not available, the Scheduled time is used.
(Note: Changes of ETA/ETD are kept in a historical structure to keep track of estimated time adjustments and refinements.)
## Flight Identifier

IATA has a well-defined method to identify a commercial flight. We adjusted the method to suit our needs.
A flight is identified by

- The operator of the flight
- The flight number
- The date/time of the departure of the flight from the origin airport in Universal Time.

The date/time used in the identifier of an arrival flight is the approximated scheduled date/time of departure of the flight from the last airport (where the flight landing at the Managed Airport is coming from, i.e. the last leg only. Example: If the flight is BOS->LHR->DOH, we use the departure time of the last leg, i.e. departure from LHR, not the departure from BOS as IATA would.)
The date/time used in the identifier of a departing flight always is the scheduled departure time from the managed airport.

Once the [[Movement|Flight Movement]] is created, an aircraft can [[Emit, Schedule, Format|broadcast]] its position.