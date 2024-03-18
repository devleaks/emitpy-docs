#flight #service 

A Flight Service is a collection of Services executed to handle a Flight.

For example, an Arrival Flight might need:

- Cleaning service,
- Sewage service,
- Cargo service to empty the aircraft.

A departing flight might need:

- Refueling
- Catering
- Cargo service to load the aircraft.


## Flight Service Scheduling

Depending on the type of Flight, Arrival or Departure, services are scheduled relative to the arrival time of the flight, or its scheduled or estimated time of departure.

For example:

- for an Arrival flight, on a remote parking, cargo offloading is scheduled to start 20 minutes *after* the aircraft is on block, the service will last 15 minutes.
- for a Departing flight, the refueling process is scheduled to start 45 minutes *before* the estimated time of departure, the service will last 15 minutes.

![[flight-service-scheduling.png]]

## Flight Service Variables

The collection of services and their timing depends on numerous parameters. In the emitpy application, we limited the dependancy on the following paramters:

- **Flight Type**: Either passenger flight or cargo flight.
- **Aircraft Type**: Wide body or narrow body. Mainly affects timing; refueling a A318 does not take the same time as refueling a A380.
- **Ramp Type**: Jetway or Tie-Down (!). Used to provide different sets of services, for example mobile staircases may not be necessary if a jetway is available; similarly, it is more likely that a fuel hydrant truck will be used on a jetway and may be some tanker trucks on remote parking location.

> Ramp type is always tie-down for cargo flights.

Rather than a fixed duration, a flight service profile may also contain a *quantity* that is used to model the duration of the service, depending on the serving vehicle.
For some services (for example Baggage Service), the service quantity is used to determine the number of round trips the baggage trolley will do between the aircraft and the baggage depot.
It is also possible to model several baggage trolley only performing one trip, or any combination of the two.

# Turnaround

A Turnaround is a collection of two flight services for an arrival flight followed by a departure flight.

# Aircraft Towing

It is possible to schedule the towing of an aircraft from the arrival ramp to the departure ramp.
Arrival Flight Services are performed at the arrival ramp. Departure Flight Services are performed at the departure ramp. (Note: Not integrated in turnaround, but can be scheduled manually.)
