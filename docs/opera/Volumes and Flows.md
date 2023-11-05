
Brainstorming.

# Raw

## Current
Number of:
1. input message
2. input message of interest
3. vehicles on the move
4. aircraft on the move




## Short Future

1. Aircraft movements expected in next 1, 3, 6 hours
2. Weather forecast (TAF) and impact on movements (change of QFU, closing of runway, larger space between aircrafts...)


# Vehicle Statistics

Observable vehicle are recorded and their movement is reported.

## Recorded Data

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

# Analysis

Rule and event data is saved and analysed by statistical and machine learning algorithms to isolate and extract values of interest.
Vehicle tracks are reconstructed and saved for processing by specialised algorithms to also extract values and information of interest.