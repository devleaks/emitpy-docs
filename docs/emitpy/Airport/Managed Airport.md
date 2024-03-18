#airport #business
The Managed Airport represents the airport that *Airport Opera* will monitor.
Emitpy will simulate activity on the ground of that airport, and generate location messages as they would be produced by vehicles on the ground or captured by ground radar equipments.

The Managed Airport is a container entity. It is responsible for loading and sharing common structures.

A first set of entities is necessary to create and simulate aircraft movements:

- The entire «[[Aerospace]]» as used in the application,
- All airports,
- Airlines, and other operators and handlers,
- All aircraft types that can be used in the application.

It then loads entities specific to the managed airport, all contained in a «[[Airport#Managed Airport Base|Managed Airport Base]]»:

- Flight procedures for departures and arrivals
- Runways
- Taxiways
- Ramps
- Aprons
- Service road network, including parking areas
- Points and areas of interest on the ground of the airport and around

A Weather Engine is created to fetch airport and en-route weather and forecasts.

Finally, it initialise the [[Airport Manager]], another containing entity responsible for airport resource allocation and monitoring:

- Runway usage,
- Ramp occupancies,
- Equipment and service vehicle use.

Once all components are loaded, emitpy is ready to create [[Flight|flights]] and [[Service|services]].