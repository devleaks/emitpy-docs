A Flight is a container entity that represent the movement of an aircraft between two airports, one of them being the Managed Airport.
There are two types of Flight:
- Arrival flights are flights that arrive at the Managed Airport,
- Departure flights are flights that leave the Managed Airport.

The creation of a flight is a 3 step process:
- Creation of the Flight Route
- Creation of the Flight Movement, including airport procedures and taxi at the managed airport
- Smoothing of the Flight Movement to make the journey more realistic.

## Flight Route
A Flight Route is a route from a departure airport to an arrival airport on the network of airway segments.
## Flight Movement
The Flight Movement is the augmentation of the Flight Route for airport specific complements.
If available, standard departure and arrival routes are added to propose a more realistic flight path. (If no procedure is available, the aircraft climbs or lands straight on the airport position, aligned with the runway if available.)
A the same time, a basic vertical navigation is added using Aircraft Performances for speeds, accelerations, and operating limits.
Finally, taxi route is added at the Managed Airport, from the runway to the parking position for arrival flights, or from the parking position to the start of the runway for departing flights.

Airspace and airway restrictions are not taken into account.
## Flight Smoothing
At this stage, the flight consists of straight flight segments with no transition. The smoothing algorithm adds a few limited adjustment to the flight path (fly-by waypoints, smooth procedure turns, straightforward transitions (direct-to), etc.)
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