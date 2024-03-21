Emitpy needs miscellaneous information for creating realistic flights or ground support vehicle movements.
# Aerospace
## Airports
### Airports
Airport need the following mandatory information:

- Name
- Municipality
- Country
- Aeronautical region
- latitude, longitude, and optionally altitude
- 
### Coded Instrument Flight Procedures

If part of a flight, it is more realist of CIFP are available at the remote airport.
CIFP are mandatory at the managed airport.

## Navigation

### Navigation Aids

Navaids need the following mandatory information:

- Name or Identifier
- Aeronautical region
- Type of Navaid
- latitude, longitude, and optionally altitude
### Fixes

Fixes need the following mandatory information:

- Name or Identifier
- Aeronautical region
- latitude, longitude
### Airways

- Name or Identifier
- Aeronautical region
- Starting and ending navaid or fix
- Restrictions (one way, upper or lower airway...)
- 
### Airspaces

- Name or Identifier
- Aeronautical region
- Restriction(s)

# Managed Airport
## Airspace
### CIFP
Arrival and departure procedure should be available at the managed airport.

### Taxiways
The network (topology) of taxiways is necessary to route aircrafts to runways and parking positions.

### Ramps
Ramps are locations where aircraft stops for servicing. A ramp has an orientation.

## Service
### Service Road (Network)
The network (topology) of service roads available to ground handling/support vehicle (GSE) is necessary to have them move on that network when travelling on the ground of the airport.

### Depots
A Depot is a special area where GSE go to do some processing with their duties. For example, it is a fuel depot where fuel tank truck go for refill, or a baggage handling terminal area where baggage trolley load or unload baggages.

### GSE Parkings
GSE Parkings are special area where GSE vehicle go when not used.

## Business
### Ground Support Equipment
#### Fleet of GSE
Determine how many vehicle of which types are available for aircraft servicing.

## Flight Services
### Arrival and Departure Services
Determine the list of services performed after an arrival or before a departure. Also specifies when the service occurs, relative to the arrival or departure times.

# Others
## Aircraft
### Aircraft Types
List of possible aircraft types for flights.

### Aircraft Performances (BADA)
Aircraft performances for each of the above type.


# Data Locations
Data like Aerospace data and aircraft performances are available throughout the application.

Data like managed airport airways, taxiways, service roads, aircraft service tasks and schedule, but also operating airlines, flight tables, etc. are specific to the managed airport.

## Reference Data

### Global Data

Aircraft types
Aircraft performances
Aircraft Ground Support Requirements (profile)
Aircraft classes

### Aerospace Data
#### Airports

#### Flexible Data
Flexible data can be aquired from different sources.

##### Airspaces
##### Navaids and fixes
##### Airways
##### CIFP

#### Managed Airport Data
##### CFIP
##### Runways
##### Taxiways
##### Ramps
##### Service roads

## Operational Data

### Companies
#### Airlines
#### Handlers
#### Operators

### Services
#### Service Types and Schedule
Arrival/departure
Passenger/cargo
Jetway/Tie-down

#### Service Vehicle Fleet

### Flight Tables
