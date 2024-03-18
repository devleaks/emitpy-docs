
# Aircraft Type

An aircraft type is a ICAO Aircraft Type Designator.
Aircraft Type also has:

- Manufacturer
- Model name
- Aircraft type (for airliners, aircraft class)

Aircraft Type optionally has:

- Number of engines
- Type of engine
- Wingspan
- Length
- Landing gear width
- A list of either alternate, or closely similar aircraft type designators
- A list of equivalent IATA aircraft type designators

### Aircraft Type Equivalence
There is a special file `aircraft-equivalence` that list ICAO and IATA code close equivalence.

```yaml
A321:
    - "321"
    - "32S"
    - "A21N"
```

### Aircraft Type
```yaml
- Date Completed: 2016-mars-16
  Manufacturer: Airbus
  Model: A321neo Sharklet
  Physical Class (Engine): Jet
  '# Engines': 2
  AAC: C
  ADG: III
  TDG: 3
  Approach Speed (Vref): 140
  Wingtip Configuration: winglets
  Wingspan- ft: 117.45
  Length- ft: 146.03
  Tail Height- ft(@ OEW): 39.70
  Wheelbase- ft: 55.45
  Cockpit to Main Gear (CMG): 44.95
  MGW (Outer to Outer): 29.43
  MTOW: 206132
  Max Ramp Max Taxi: 207014
  Main Gear Config: D
  ICAO Code: A21N
  Wake Category: M
  ATCT Weight Class: Large Jet Eqpt
  Years Manufactured: tbd
  Note: tbd
  Parking Area (WS x Length)- sf: 17 151
```


# Aircraft Class
The Aircraft Class is an aircraft attribute based on aircraft length and/or wingspan.
There is a procedure to attempt to automagically determine the class of an aircraft.

The Aircraft Class is used as a fall back aircraft model when some data is missing.

An Aircraft Class is an Aircraft Type with special keyword *class* `CLASS` and a keyword *type*  `A`, `B`, `C`, `D`, `E`, or `F`.

When the aircraft class cannot be found, aircraft class `C` is used.

For a given class, all data from a typical aircraft of that class is used. There is a class for équivalence in Airbus aicraft models, and one for Boeing aircraft models.

| class | Airbus    | Boeing   |
| ----- | --------- | -------- |
| A     | A318      | B731        |
| B     | A320      | B737-800 |
| C     | A321neo-LR      | B787     |
| D     | A350-900 or A330-800 | B777-300     |
| E     | A340-600      | B747-800     |
| F     | A380-800      | -        |

# Aircraft With Performance
An aircraft with performance is a Aircraft Type augmented with Eurocontrol BADA performance data. Performance data is almost exclusively kinematic.

```yaml
A21N:
  icao: A21N
  iata: 32Q
  takeoff_speed: 145
  takeoff_distance: 2150
  takeoff_wtc: M
  takeoff_recat: Upper Medium
  takeoff_mtow: 97000
  initial_climb_speed: 175
  initial_climb_vspeed: 2000
  climbFL150_speed: 290
  climbFL150_vspeed: 1500
  climbFL240_speed: 290
  climbFL240_vspeed: 1200
  climbmach_mach: 0.78
  climbmach_vspeed: 1000
  cruise_speed: 450
  cruise_mach: 0.78
  max_ceiling: 390
  cruise_range: 4000
  descentFL240_mach: 0.78
  descentFL240_vspeed: 1500
  descentFL100_speed: 290
  descentFL100_vspeed: 2500
  approach_speed: 250
  approach_vspeed: 1300
  final_speed: 210
  landing_speed: 140
  landing_distance: 1850
  landing_apc: C
  wingspan: 35.8
  length: 44.51
  height: 11.76
```
# Aircraft
An Aircraft is an airframe with a registration number and an ICAO 24bit hexadecimal ADS-B emitter address. It may also contain its serial number if available.

# Aircraft Ground Support Equipment Profile

The Aircraft Ground Support Equipment Profile is a set of 3D oriented positions relative to the tip nose of the aircraft. These positions are used to place ground support equipment vehicle around the aircraft frame.
There is such a file for each AircraftType. If a profile cannot be found for a precise aircraft type, a profile is searched for similar types. If no profile can be found, the class profile is used. If no class profile can be found, the default, standard, always available class `C` is used.

```yaml
ac-type: A320
services:
    sewage:
      - 35
      - 0
      - 90
    cleaning:
      - 30
      - 25
      - 0
    catering:
      - 32
      - 5
      - -90
    fuel:
      - 15
      - 10
      - 90
    fuel2:
      - 15
      - -10
      - -90
    water:
      - 35
      - 4
      - 90
```

```yaml
service-type:
	- distance-from-nose-along-aircraft: 13.5 # meters
	- distance-from-longitudinal-axis: 4.7. # meter
	- orientation-of-vehicle-relative-to-aircraft # degrees
	- optional-height-for-contact: 6.4 # meters AGL
```