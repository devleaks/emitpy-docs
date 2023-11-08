
A Rule correspond to a movement of interest that needs monitoring.

A Rule first specifies which vehicles need monitoring and then details which types of movements need reporting. To precise the movements, a Rule uses two *Events*, a start event that dictates when the monitoring of the movement must start, and an end event when the movement no longer need to be monitored.

# Events

An Event occurs when a [[Vehicle|vehicle]] makes an *action* relative to an [[Areas of Interest|Area of Interest]].
Opera constantly monitor vehicle movements and raises events as they occur.

## Actions

Possible vehicle actions relative to areas of interest are:

- Entering (an area of interest)
- Leaving (an area of interest)
- Being stopped inside an area of interest
- Crossing an area of interest.

Actions are determined on the basis of the penultimate and the last known position of a vehicle. For example, when a vehicle is not in an area of interest in the penultimate position, and inside an area of interest in the last position, we assume the vehicle *entered* the area of interest.

When the position of a vehicle has not changed between reported positions, or when the average reported speed of the vehicle is close to 0, or the relative distance between the two reported positions is small, we assume the vehicle has *stopped* in the area of interest. 

Finally, all areas of interest that are intersected by the line joining the penultimate and last positions, we assume they are/were *crossed* by the vehicle, assuming the vehicle move onto a straight line between the last two points. In practice, the penultimate and last position must be outside the area of interest and the line joining the penultimate and last position must have at least one intersection point with the area of interest.

![[events.png]]

> For most events, crossing points between vehicle trajectories and areas of interest are recorded and it is possible to determine timing information if necessary.

## Areas of Interest

Areas of interest are polygons on the ground of the airport. They can be as large as the entire airport or as small as a parking location.

Areas of interest are named following the same identification mechanism as vehicle, using four attributes. This allow for basic areas of interest grouping, by classes or types.

When writing an Event, it is not necessary to supply a single, [[Areas of Interest#Area of Interest Identification and Grouping|unique area of interest]]. It is possible to supply a collection of areas of interest (AoI). The Event will match any AoI that is in the collection.

# Rule

A Rule is a coordination of two events for a vehicle, or category of vehicle.

## Name

Each Rule has a name for identification purpose. It usually is a serial number.
If the name of the Rule starts with `#`, the Rule is ignored (commented out).

## Vehicles

When writing a Rule, it is not necessary to supply a single, unique vehicle identifier. It is possible to supply a **type** and/or a **class** of vehicles. The Rule will match any vehicle that is in the collection. Examples of vehicle classes are aircrafts, or ground support vehicle. Examples of vehicle types are aircraft models or ground support vehicle function like refueling or baggage handling.

In a Rule, the vehicle is specified as a regular expression that must match the vehicle identifier.
## Areas of Interest

In a Rule, the collection of areas of interest is specified as a regular expression that must match the area of interest identifier.
## Start and End Events

A Rule is defined by two events of interest, a *start* event and an *end* event.

For example:

- Start: When a vehicle exits any runway
- End: When a vehicle enters any ramp

## Rule Timeout

The rule has a timeout that is started when the start event occurs and determine the time before which the end event must arrive.
The rule will always remain active until it times out, even if its end event(s) occurred.
The timeout is reset each time the start event of the rule occurs.

# Rule Monitoring

Each time a new position arrives, Opera determine the vehicle and monitor whether the vehicle triggers some Events.
## Event Message

A vehicle making an action relative to an area of interest produces a Message with:

- The vehicle identifier,
- (The position of the vehicle,)
- The time of the last event,
- The action,
- The area of interest that is involved.

If a triggered event is part of a Rule, the Rule is updated as follow:
## Promise

When an event matches the *start* event of a rule, the rule is **activated**. The rule becomes a *promise* for a precise vehicle and area of interest.
The Rule remains a promise until the rule times out. The timeout is reset each time the same start event occurs, for the same vehicle, for the same area of interest.

## Resolution

When an event matches the *end* event of a Promise, the rule is **resolved**. The result of the rule is archived for later processing.

When a rule is resolved, its promise is not removed. The promise remains until it times out.

## Resolved Rule Data

When a rule is resolved, the following data is stored:

- Identifier of the rule,
- Event data of the promise,
- Event data of the resolution.

The most valuable data that is retained is the time difference between the *promise* and the *resolve*, in other words, the duration of the rule.

