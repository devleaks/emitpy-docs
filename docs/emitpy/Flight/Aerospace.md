#flight #airspace #aerospace
The Aerospace entity is a container entity for everything related to aerospace where aicrafts can fly. It contains:
- Terminals (airports),
- Navigational aids,
- Fixes, waypoints,
- Airways, optionally with their restrictions,
- Holds,
- Airspaces, optionally with their restrictions.

> [!NOTE]
> Note: The container class name Aerospace has been used since release 0.12 to distinguish from Airspaces which have a precise and well defined meaning in aeronautics.
## Aerospace

The Aerospace is an abstract base class to define Aerospace for emitpy.
An aerospace must contain the following data

- Navigational aids,
- Fixes and waypoints,
- Airway segments between navaids and/or fixes.

but this data can be aquired from different sources.

An Aerospace is a (network) graph, with navaids and fixes being vertices and airways being edges.

The aerospace graph is used to find routes between airports using airways. (Ultimately, if no route can be found between two airports, a direct grand circle arc can be used between departure and arrival airports.)