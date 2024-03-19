To enhance movement realism, emitpy needs a few named points of interest as destination.
It is not possible to find those points in any database.
We recommand using a tool like geojson.io to create a GeoJSON FeatureCollection with all named point. Point must be attached a few GeoJSON Feature properties to identify and qualify them.

# Service Roads

## Service Depot
For a give service, a depot is the location from which all service vehicle will start.
There may be more than one depot for a given service.
A depot may be used by one type of service only.

### Properties
type: depot
service: list of `|`-separated service names.
name: optional depot name, if not provided, a default name will be generated.

## Service Rest Area
A Rest Area is a point where service vehicle go when they do not provide a service. Alternatively, they may also go to a depot.
There may more than one rest area for a given service.
A given rest area may be used for different services.

### Properties
type: rest-area
service: list of `|`-separated service names or  `*` for all services.
name: optional rest area name, if not provided, a default name will be generated.

## Mission Checkpoint
A Checkpoint is a named point of interest on the service road network.
There currently is only one type of check point.
It is possible to name them in such a way that they exhibit some category.
For example: security:gate:west-5, or cargo:custom:landside-4.

### Properties
type: checkpoint
service: mission
name: optional checkpoint name, if not provided, a default name will be generated.

# Aeroways

## Runway Exit
Runway exits are difficult to identify (need network analysis).
For smiplification, it is advisable to provide a list of runway exits on either side of the runway.
When an aircraft ends its landing roll and reaches a speed of about 50km/h (~ 30kn) or less, it may exit the runway towards the network of taxiways.
Runway exit points are named after the runway: `RW34L:exit:5L` is the same as `RW16R:exit:3R`.

### Properties
type: runway-exit
runway: Runway name format `RWnn{LCR}`
name: optional runway exit name, if not provided, a default name will be generated.
side: left or right, relative to aircraft direction (optional)

> Emitpy tries to locate runway exists by finding taxiway nodes close or on the runway. However, this procedure sometimes fails, resulting in a runway with no exit point. In this case the only exit is at the runway end. (Opposite take-off hold position.)

## Take-Off Queue Point
A Take-Off Queue point is a fixed position where an aircraft stops when queueing for take-off.
Take-Off Queue Points are built as regularly spaced points on a line string.
For each runway, it is necessary to supply a linestring that starts at a the runway take-off hold position, and that runs backward towards the terminal areas. Emitpy will create queueing positions from the take-off hold position (queueing position 0), at regular intervals (parameter QUEUE_GAP ≃ 200 meters), until the end of the supplied line string. If the supplied line string is shorter than the QUEUE_GAP, only one queueing position is created (0) at the the take-off holding position.
If no linestring is supplied, emitpy will try to run backward on taxiways from the take-off hold position, to create at least 1 queueing position. However, this position may end up in a unwanted place on the taxiway network (that is runway included if runways can be used for taxiing).

> In all cases, at least one queueing position is created (0) at the the take-off holding position, which the destination of aircraft taxiing for take-off.

Please note that aircrafts always take off from the beginning of the runway.