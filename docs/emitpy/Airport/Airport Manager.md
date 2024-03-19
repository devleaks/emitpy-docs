The Airport Manager is a containing entity that is responsible for managing resources used by the simulation.

The Airport Manager contains

- The fleet of service vehicles, grouped by service vehicle types (catering, fuel, etc.), their usage and availability for service,
- All ramp allocations for turnaround operations,
- All runways allocations for take-offs and landings.

It registers usage of resources like runways, ground vehicles or ramps.

The Airport Manager also contains reference data for the simulation:

- Operating airlines and their air routes to/from the Managed Airport
- A directory of all companies operating at the Managed Airport (airlines, handlers, or other services like firefighting, custom, or police.)

Resource allocation can be changed, however, there is no check that the new requested times are available for the resources. A resource scheduler is a complex software on its own and we could not find one to use with Emitpy.
