A movement is a time-ordered collection of positions that represent the displacement of a vehicle. Each position is associated with properties like speed of the vehicle at the position. Geometry-wise, it can be considered as a augmented LineString.
A movement has no absolute time. All times in a movement are relative to the start of the movement. A movement can then be scheduled to occur at any time. The movement will never change, only the time at which it occurs. Deciding the time at which the movement will occur is the purpose of the *movement scheduling*.
# Emit
The Emission of a Movement is the process of creating an alternate movement representation that follow the exact same path, but where position points are equality distant in *time*, the difference in time between two position is always the same.
That difference in time between two positions is called the *emission time*.

![[flight-movement2.png]]

The resulting path is called the *Emit*. Very much like a flight movement, an Emit is not time dependant. Each point occurs the same time period after the preceding one. Deciding the time at which the emission will occur is the purpose of the *emission scheduling*.
## Emit Frequency
Emit is the process of broadcasting position information for a Movement at regular time interval.
Emit starts from a Movement. It follows the movement, taking into account the movement times and speeds, and insert emission marks at regular time interval. The time interval is a parameter of the Emit process. It can be as frequent as every second, or as infrequent as every 10 or 30 minutes.
The result of the Emit process is a new collection of time-ordered positions, positions where the emission of the position will occurs. Geometry-wise, it can be considered as another LineString where there is exactly the same time interval between each position if we consider that the LineString represents a movement of a vehicle.

The same movement can be emitted several times with different emission parameters.

The result of Emit, the new LineString, is also time-relative, with the time zero at the beginning of the Movement.

The Movement LineString and the Emit LineString have the same path in space.

During the Emit process, [[Movement#Mark|Marks]] are preserved with their precise time and location.
## Emit Frequency Limit
When the emit frequency is higher than every 10 seconds, emission will only occur if the vehicle is in the vicinity of the Managed Airport.
Typically, when simulating the echo of a radar ping, ground radar broadcast the position of vehicle every second. This can produce a significant amount of data, both during the movement and emission generation process and during the broadcast of the messages on an output queue.
Example:
- 8 moving aicrafts, and
- 20 parked aircrafts all being services by 4 service vehicles each,
approximately generate 100 messages per second.
For a intercontinental 8 hour flight, we will not generate positions every second. We will only generate positions every second if the aircraft is less than 3 or 5 nautical miles from the simulated radar of the managed airport.
# Scheduling
Scheduling is the process of setting an absolute time of emission for each Emit.
To schedule an Emit, it is necessary to supply a Mark and the date/time at which the Mark is reached.
For example, for a flight, we can schedule the emission such that the touch-down time is a very precise date/time. For a service, we can schedule de service such as the end of the service terminates 15 minutes before the departure time.
# Format
The Format process generates the simulated message from data avaialble in emitpy.
In the course of building the movement, data is accumulated at each point: position, speeds, timing information, aircraft used, service vehicle type...
A standard ADS-B message does not contain all this data. There is a step to select which data will be broadcast, and in which format. That process is called the Formatting.
## Default Format

#### Default Format for Positions
The default format is text, each point is published as a GeoJSON Feature point with all data as name,value pair properties. This format is called `raw`. Structured properties can optionally be flattened into a simpler (name, value) structure. In this case, the format is called `flat`.
#### Default Format for Messages
The default format for Messages is text. A dictionary of (name, value) pairs published as a JSON text string.

Formatted messages are then stored for later [[Broadcast|broadcast]].

# Re-Schedule

## ReEmit

When an Emit is rescheduled, *absolute emission times* are changed but all other attributes are unaffected. A *ReEmit* loads an existing Emit (from a file or from Redis database) and re-schedule it.
If the emission was enqueued for broadcast, emission points with the old schedule are removed first and the new scheduled points are enqueued.

The same applies to accompagnying Messages that are re-scheduled accordingly. See  [[Message#Message Scheduling|ReMessage]].