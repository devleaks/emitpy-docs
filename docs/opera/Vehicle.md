A Vehicle is a generic term for a device that moves on the ground of the airport and regularly reports its position. A Vehicle can be a ground support vehicle or an aircraft.

When Opera receives a new position, it first identifies the Vehicle that reported its position.

# Vehicle Identifier and Grouping

Most, if not all objects in Opera are identified by [[Identity|4 identifiers]]. These identifiers are used to group and organize objects in collections.

For example, for Vehicles, the four identifiers can be used as such:

| orgId    | classId | typeId  | name   | description                                 |
| -------- | ------- | ------- | ------ | ------------------------------------------- |
| British Airways | C       | A321    | OO-PMA | Airbus A321 with ICAO24 registration efface |
| StandardOil  | fuel    | hydrant | FUEL07 | Fuel vehicle ICAO24 aabbcc                  |
| LAPD  | Security | police  | POL123 | Mission patrol vehicle ICAO24 abacad        |
|          |         |         |        |                                             |

The combination of these four attributes make the *Vehicle Identifier*.

## Vehicle Attributes

### Key

The key of a vehicle is its ICAO24 ADS-B address in hexadecimal format (6 hexadecimal digits).

### Identifier

See above.

The identifier is used to uniquely identify an object.

### Is Aircraft

There is a distinction between aircrafts and ground vehicle or personnel.

