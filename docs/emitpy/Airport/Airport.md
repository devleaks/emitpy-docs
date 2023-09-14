#airport
## Airport
In its simplest form, an Airport is a localized named entity. It contains:
* Its position (lat, lon, alt)
* Its administrative location (city, country)
* Its timezone


## AirportWithProcedures
In a more complex form, an airport can be fit with its *Coded Instrument Flight Procedures*. Procedures include:
- Runways
- Standard Instrument Departure Procedures (SID)
- Standard Terminal Arrival Procedures (STAR)
- Approaches (APPCH)

Sometimes, noticeable transitions are also included.


## Managed Airport Base
In its most complex form, an airport references all additional data necessary to qualify as a Managed Airport.

The Managed Airport Base is an abstract class that can be used as the base of Managed Airport. Realisation of the abstract class are responsible for loading and providing necessary data. A Managed Airport must contain the following data:
- Runways
- Network of taxiways
- Ramps
- Network of service roads
- Points of interest

This data can be aquired from different sources.