A Rule is a pair of matching *events*.

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

## Event Data
An Event produces the following data:
- The vehicle identifier,
- (The position of the vehicle,)
- The time of the last event,
- The action,
- The area of interest that is involved.

## Vehicles
When a new position arrives, the vehicle identifier is extracted. (The vehicle identifier often is the ADS-B hexadecimal address.) The identifier is looked up in a identifier database and the vehicle meta data is associated with the event: Vehicle type, function, model, other identifiers or call signs, some physical characteristics, etc.

If it is an unknown vehicle identifier, Opera will try to guess the vehicle type from its behaviour and complement some characteristics that can safely be deduced.

The most important characteristics of a vehicle are its **class** and **type**.

When writing a Rule, it is not necessary to supply a single, unique vehicle identifier. It is possible to supply a **type** and/or a **class** of vehicles. The Rule will match any vehicle that is in the collection. Examples of vehicle classes are aircrafts, or ground support vehicle. Examples of vehicle types are aircraft models or ground support vehicle function like refueling or baggage handling.

# Areas of Interest

When writing a Rule, it is not necessary to supply a single, [[Areas of Interest#Area of Interest Identification and Grouping|unique area of interest]]. It is possible to supply a **named** collection of areas of interest (AoI). The Rule will match any AoI that is in the collection.

# Rule

A Rule is a coordination of two events.
## Definition
A Rule is defined by two events of interest, a *start* event and an *end* event.
For example:
- Start: When a vehicle exits any runway
- End: When a vehicle enters any ramp
To further refine the rule, we can require that the vehicle be of a certain type, like an aircraft.
The rule also has a timeout that is started when the start event occurs and determine the time before which the end event must arrive.
The rule will always remain active until it times out, even if end event(s) occurred.
The timeout is reset each time the start event occurred.
## Promise
When an event matches the *start* event of a rule, the rule is activated. The rule becomes a *promise* for a precise vehicle and area of interest.
The Rule remains a promise until the rule times out. The timeout is reset each time the same start event occurs, for the same vehicle, for the same area of interest.

## Resolution
When an event matches the *end* event of a promise, the rule is *resolved*. The result of the rule is archived for later processing.
When a rule is resolved, its promise is not removed. The promise remains until it times out.

## Resolved Rule Data
When a rule is resolved, the following data is stored:
- Identifier of the rule,
- Event data of the promise,
- Event data of the resolution.

The most valuable data that is retained is the time difference between the *promise* and the *resolve*, in other words, the duration of the rule.

# Analysis

Rule and event data is saved and analysed by statistical and machine learning algorithms to isolate and extract values of interest.
Vehicle tracks are reconstructed and saved for processing by specialised algorithms to also extract values and information of interest.
