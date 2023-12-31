Opera monitors vehicle movements through areas of interest. Areas of interest are polygons on the ground of the airport. Polygons are named and combined through their class and type identifiers (See below).

Here are the typical areas of interest defined in Opera:

- Runway
- Taxiway segment (buffer of `taxiway_width`  around the 2 point segment)
- Service road segment  (buffer of `service_road_with` (contant) around the 2 point segment)
- Ramp
- Apron
- Terminal
- Service depot
- GSE Parking
- Checkpoints
- Airport areas
- Aerodrome
- TMO and more

# Collection of Areas of Interest

Individual areas of interest are grouped in "functional" categories.

- Ramps
- Taxiways
- Service roads
- Aprons
- GSE Parkings
- Airport sections

Finally, areas of interest may be grouped by other criteria such as
- Frequently visited area
- Areas in same vicinity (proximity), like neighboring areas

# Area of Interest Identification and Grouping

Most, if not all objects in Opera are identified by [[Identity|4 identifiers]]. These identifiers can be used to group and organize areas of interests in collections.

For example, the four identifiers can be used as such

| orgId   | classId | typeId  | name      | description                               |
| ------- | ------- | ------- | --------- | ----------------------------------------- |
| airport | aeroway | runway  | 34L       | A runway                                  |
| airport | aeroway | runway  |           | *all* runways                             |
| airport | aeroway | apron   |           | *all* aprons                              |
| airport | aeroway | environ | TMO       | Circular zone 10 miles around the airport |
| airport | aeroway | ramp    | E17       | Aircraft parking E17                      |
| airport | service | depot   | Catering1 | First catering restaurant                |
| airport        |service         |depot         |Fuel           |Main airport fuel depot                                           |

# Area of Interest Statistics

The following information may be recorded for each area of interest:

- Timestamp of last vehicle entering the area
- Total number of vehicles in area
- Total number of vehicles traversing the area (during a given timeframe, like 15 minutes, or a moving average of the number of vehicles traversing the area.)

