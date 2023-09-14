# Vehicle Identifier and Grouping
Most, if not all objects in Opera are identified by [[Identity|4 identifiers]]. These identifiers can be used to group and organize vehicles in collections.

For example, the four identifiers can be used as such

| orgId    | classId | typeId  | name   | description                                 |
| -------- | ------- | ------- | ------ | ------------------------------------------- |
| aircraft | C       | A321    | OO-PMA | Airbus A321 with ICAO24 registration efface |
| service  | fuel    | hydrant | FUEL07 | Fuel vehicle ICAO24 aabbcc                  |
| service  | mission | police  | POL123 | Mission patrol vehicle ICAO24 abacad        |
|          |         |         |        |                                             |




# Vehicle Statistics
Observable vehicle are recorded and their movement is reported.

## Key
The key of an observable vehicle is its ICAO 24 bit transponder address.

## Recorded Data
### Vehicle
Vehicle type
- Aircraft
- Service
- Mission

### Position
When a vehicle broadcast its position, the following information is recorded:
- timestamp of *reception* of message by Opera
- ICAO address
- position (latitude, longitude)
- altitude if available
- speed if available
- timestamp of *emission* of message if available

Redis Key: `vehicle:lastpos:icao24`

## Position Analysis

### Areas
In addition to the preceeding data, the following is immediately associated with the vehicle:
- Inside:
	- Timestamp
	- (Airport) areas of interest (identifiers) where the vehicle is inside.
- Crossed:
	- (current timestamp, time elapsed since last timestamp)
	- (Airport) areas of interest (identifiers) that intersect the line between the last known position and the current position. 

### Stopped
We determine if the vehicle is moving or stopped.
(Algorithm needs refinement.)

If stopped on parking area or near aircraft parking/apron: notifies, but behavior acceptable.
If stopped (for a long time) on a service road not on a parking area: raise warning.

### H3
We record the [H3](https://h3geo.org) index (level 14, 6sq.meter resolution for hexagons) where the vehicle is located.

## Behavior Analysis

### Observations
Observations over last *x* minutes:
1. Average speed if not stopped
2. Average speed if not parked (parked = stopped in designated parking area)
3. Average distance covered
4. Average time stopped/in movement (ratio)

### Reports

