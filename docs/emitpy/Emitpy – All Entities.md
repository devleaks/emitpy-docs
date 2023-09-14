# Core Entities

1. The [[Managed Airport]]

# Flight

1. [[Aerospace]]
    1. Navaids and fixes
    2. Airways
    3. Airspaces
    4. Airport (terminals)
    5. Terminal Procedures
    6. Runways
    7. Taxiways
    8. Ramps
    9. Aeroway Points of Interest (POI): Runway exit, taxi hold positions.
2. [[Aircraft]]
3. [[Flight]]


# Ground Support

1. [[Service]]
1. [[Equipment|Equipment]]
1. [[Flight Service]]
1. [[Flight Service#Turnaround|Turnaround]]
1. [[Mission]]
1. [[Service#Ramp Service Location|Ramp Service Point Profile]]
1. Service roads


# Movement

1. [[Movement]]
2. [[Message]]
3. [[Emit, Schedule, Format]]


# Communication and Broadcast

1. [[Broadcast]]: Queue and Formatting

# Notes

A few real-life objects or concepts exist and are represented by different entities depending on their function in emitpy.

For example, an *airport* is represented as
- a geographic named entity called an Airport (latitude, longitude, altitude, time zone, city, country),
- a aeronautical named entity called a Terminal (CIFP procedures, available runways…).

Similarly, an *airport runway* is represented as
- a named geographic entity (either a line or a polygon surface) called a Runway,
- a named aeronautical entity (heading, length…) called RWY,
- a resource (usage, time slots), called a RunwayResource.
(When grouped in collections, containers wear names like `runways` , `rwys`, or `resource` to distinguish between the two.)

A *ramp* is represented as
- a named geographic entity (lat, lon, heading) called a Ramp,
- a resource (allocation, time slots).

Often, if convenient, both entities are linked together.