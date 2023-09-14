
A *Message* is an entity that is broadcast on a special queue called *The Wire*. All messages are sent on The Wire.

Message are mainly created for notification of information purpose.

Each entity can have its Messages associated with it:
- Flights
- Missions
- Services
Each of the above core entity, its associated movements or emissions, each has its own set of messages. A dependent entity includes the messages of its parent entity. A Movement has its own set of messages and includes those of the parent core entity. A Emit has its own set of messages and includes its parent movement entity. At the end, it is the collection of messages of the Emit that is sent to *The Wire*.

# Messages
Here is a list of messages that are created and published.

For aircrafts and their movements:
- ACARS OOOI messages
- Notification of flight rescheduling or ETA/ETD adjustments

For services and their movements:
- Start and end of service.

For Missions and their movements:
- Start and end of Missions
- Arrival at Mission Checkpoint

Additionally, emitpy generates a few *internal* messages like:
- occasional broadcast of each queue current date/time,
- queue creation and suppression,
- operational messages related to the simulation.


## Message Scheduling

Messages are scheduled (and rescheduled) to remain synchronized with their corresponding source (often a movement).

When re-scheduled, a *ReMessage* loads an existing message (from the file or Redis database) and its absolute emission time is re-calculated. It is saved with its new schedule, and enqueued for broadcast with its new emission time.

See also [[Emit, Schedule, Format#ReEmit|ReEmit]].