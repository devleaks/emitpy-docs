# Aircraft

An Aircraft is entity that reprensent a precise frame.
An aircraft has

- A registration
- An optional initial registration or serial number
- An ICAO24 bit address, often presented as a 6 hexadecimal character suite,
- but most importantly, has an **Aircraft Type** (*with performance* data associated to it).

It can also contain other properties like its seating or cargo configuration.
# Aircraft Type

The Aircraft Type is a named entity.
Common aircraft types in ICAO DOC8643 are loaded, together with their IATA code if available.

There is a Aircraft Type equivalence, to link similar aircrafts together, either through their IATA code or their ICAO code.

# Aircraft Type with Performances

Common aircraft types used for civil aviation are loaded together with their performances as extracted from Eurocontrol Aircraft Performance Database (BADA).

# Aircraft Class

Each Aircraft Type with Performance is assigned a class (Letters A (small) to F (A380)) based on their wingspan and length.
An Aircraft Class is a Aircraft Type with Performance for a group of similar aircrafts representing similar physical characteristics and performances.
When characteristics for an aircraft are not found in its Aircraft Type with Performance, data is looked up in its Aircraft Class.

```python
# ws = wing span in meters
    try_class = "A"
    if ws > 78:
        try_class = "F"
    elif ws > 65:
        try_class = "E"
    elif ws > 50:
        try_class = "D"
    elif ws > 40:
        try_class = "C"
    elif ws > 32:
        try_class = "B"
```

# Aircraft Ground Support Equipment Profile

An Aircraft Ground Support Equipment profile list all GSE and where they should be positioned relative to the aircraft's nose tip (= (0, 0), left, relative to aircraft direction is *x* negative values, right is positive values, in front of aircraft *y* is negative value, on the aircraft side it is positive value.

The profile depends on the model of the aircraft.
If the profile is not available for the model of the aircraft, there is a fall-back on the class (A-F) of the aircraft. If a class of aircrafts is not found, there is fallback on class C which is always available and defined. (Class C is the largest narrow body aircraft type.)

# Aircraft Turnaround Profile

An Aircraft Turnaround Profile list all tasks that occurs during a turnaround.

The profile depends on
1. the direction of the flight: arrival or departure
2. the type of flight: cargo or passenger
3. the type of the ramp: jetway or remote parking (called tie down)
4. the model of the aircraft, or it’s class,
5. the airline or ground handling company operating the flight or the turnaround

If one of the above depending data is not available, there always is a fall back solution ultimately selecting a class C aircraft being serviced for cargo or passenger at a gate or tide-down remote parking.
