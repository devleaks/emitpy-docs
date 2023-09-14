#airport #business #resource

An Equipment is a hardware resource that is used by service, typically Ground Support Vehicle. The vehicle reports it’s position so that it can be integrated into Opera analysis.

(will be detailed later, to do)

# Goods and Services

An equipment has a capacity expressed by 4 values that can be adjusted to provide realistic service times.

## Parameters
### Maximum Capacity
The maximum capacity of a vehicle.
Example: Fuel truck 30kLiters, baggage train: 100 cases.
### Flow
The time it takes to process one unit of good. Expressed un UNIT per SECOND
Example: Fuel flow: 0.6L per second, baggage: 1 baggage every 5 second.
### Setup and Cleanup Times
Time to prepare the service, or to clean it up when completed.

## Working Variables

### Current Load
How much unit of good in the vehicle.
Example: Fuel: Truck has 23455L left. Example Baggage: Train has already 60 cases.

## Requested Service Variables

### Quantity
The quantity of good to deliver or capture.
Example: Fuel: 20000L, Baggage: 250 cases, cargo: 30 ULD.


## Deduced Variables

### Time to service
time to setup + quantity / flow + time to cleanup. + time to round trip to a depot (and refill/unload) if service cannot be completed in one « trip ».
The service can also be a fixed time. Like GPU setup: 3 minutes.


# Movements

A Vehicle has 3 speeds:

1. Fast, when on service roads, between parking, depots, and apron.
2. Normal, when on an apron.
3. Slow, when closing to the aircraft to/from a service position.

