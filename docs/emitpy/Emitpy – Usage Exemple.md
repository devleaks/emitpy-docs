Practically, currently, the emitpy generator can be used from two end points.

# Python EmitApp Class
First, there is a wrapping EmitApp python class that loads all necessary entities and offer a limited number of entry points to generate flights and ground support equipment movements.

- do_flight
- do_service
- do_flight_service
- do_schedule
- do_mission

And their deletion counter parts


All function parameters are strings.


# REST API
As an alternative to this python class that can directly be used in python scripts (numerous examples are provided in the `bin` directory), emitpy proposes a very simple direct REST API to execute the very same calls. The REST API also has numerous information end points to get, for example, a list of valid aircraft type or fuel vehicle models. Those information end points can be used to build user interfaces. A Postman file has example of API call and there is also a script of direct calls to the API to exemplify its use. 

# Examples

## Single Flight

## Turnaround

## Flight Table

## Day Activity


# Practical Use
The original design goal of Emitpy was to generate the difficult to get ADSB-B messages. Emitpy was created to artificially generate those messages. To do so, the idea is to proceed as follow:
1. When the flight board is available, arrival and departure flights can be created as scheduled. Creation can proceed until emission points are ready to be used.
2. When some estimated or actual position is received for a flight, for example, when the aircraft took off, or when we receive and ACARS message, or when we receive an ETA, etc. we can take the set of emission points generated at step 1 above and schedule them to fit the received position, to fit the reality.
3. ADS-B messages will be enqueued by Emitpy as they would be produced by the aircraft and capture by a local ADS-B message receiver. They can be processed and used like real messages.

# Possible Failure

Here are the most common reasons for failure:

1. Non existant airport (changed, new, abandoned, due to discrepency between flights, flight tables, and aeronautical databases used.)
2. Invalid METAR or TAF message (failure to fetch data, failure to parse returned data)
3. No route found for a flight using airways.
4. No route found for a service vehicle on service road network.

Sometimes, simply re-submitting the same request will work without error, probably because some random combinations of parameters have caused the issue.

We have a set of ~250,000 movements that we generated with emitpy.
Statistically, more than 92% of generation succeed. It is rare to find a failure not enumerated above.

