The following note is a description of the steps needed to use Emitpy effectively.


# Initialisation

When using Emitpy, the first step is to create the environment where vehicle movements will be created. This consists of
- Initiating the Aerospace where flights will occur,
- Initiating the Managed Airport where ground support vehicle will move,
- Selecting a few options regarding the environment, like the source of weather information if desired.
This has to be done once, the environment will be used over and over again afterwards.

# Flight Elements

Before we can create a flight, we have to collect all elements necessary for it.
- Airports, one of which will be the Managed Airport,
- Aircraft, from its aircraft type,
- Local details like parking ramp and/or gate,
- General flight informations like flight level and cruise speed,

If necessary, it also is possible to enforce one or more flight procedures used at each airport.

When all data is collected, a new flight can be created.

# Flying

When the flight has properly been created, it can proceed with its movement, it’s scheduling, and ultimately, the production of ADS-B messages that will be emitted during the flight.

Later, the flight can be rescheduled.

At this stage, it is not possible to change a flight data or parameter once it is created. A new flight has to be created.

# Ground Service

Once a flight has been created and scheduled, it is possible to create and schedule all services at the managed airport.


# Learning

At the root of the source code of Emitpy, there are two scripts that can be used to learn how to create flights with Emitpy.

`Loadapp.py` is a script that loads data from Emitpy and save it to a Redis database (simple key, value store).

`Emitapp.py` is a script that chains necessary operations to create flights and ground support services.