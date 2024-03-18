Graphs are used when it is necessary to find a Route between two points close to the graph.

1. Navaids, fixes and airway segments form the Airspace graph.
2. Taxiways and ramps form the Taxiway graph.
3. Service roads, ramps, and points of interest for the Service Road graph.

In emitpy, a Graph is a collection of Vertices (Vertex, a GeoJSON Feature< Point >) and Edges (Edge, a GeoJSON Feature< LineString >). An Edge exposes its extremities (`begin` and `end`). Edges are directed.

Vertices and Edges have additional properties like the `usage` property that list one or more use of the vertex or edge.

While graph entities remain custom classes in Emitpy, each contain a networkx Graph representation that is used to find routes.
## Route

A Route is a list of segments (Edges) to go from a source vertex to a destination vertex.
Most of the time, the A-Star algorithm is used with the distance used as a heuristic function since all graphs in emitpy are geolocalized.