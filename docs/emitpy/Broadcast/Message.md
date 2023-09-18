
A *Message* is an entity that is broadcast on a special queue called *The Wire*. All *Messages* are sent on *The Wire*.

Message are mainly created for notification of information purpose. Any entity can have Messages associated with it:
- Flights
- Missions
- Services
Each of the above core entity, its associated movements or emissions, each has its own set of messages. A dependent entity includes the messages of its parent entity. A Movement has its own set of messages and includes those of the parent core entity. A Emit has its own set of messages and includes its parent movement entity. At the end, it is the collection of messages of the Emit that is sent to *The Wire* after scheduling.

The core work of emitpy is to broadcast positions of vehicle (together with meta-data), messages is another set of data that can be broadcast but does not carry a position, only a time of emission, absolute, or relative to the movement it relates to.

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


## Message Text
Messages have
- a mandatory Subject
- an optional Body
- an optional link
- meta-data, including status and priority.


## Message Categories
Messages have a type:
- normal (as produced by emitpy entities to communicate their evolution)
- operational (about the behavior of emitpy)
- internal (about the internal behavior of emitpy)

Inside each type of message, messages belong a a category to determine its use. For example, normal messages can below to
- ACARS OOOI message,
- flight board message to display flight status evolution, scheduling, delays...,
- service messages to communicate a service has started or ended,
- ...

## Message Decorations

Messages contain a few decorative attributes to help presentation.
- Icon
- Color
