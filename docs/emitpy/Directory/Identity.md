
An Identity is the base class for named entity in the emitpy application.
It contains the following mandatory attributes:

- A Organisation Identifier `orgId`
- A Class identifier `classId`
- A Type identifier `typeId`
- A name `name`

> The four attributes were inspired years ago by a IBM IoT naming scheme and allow for fine flexible naming and classification. The original identifiers were orgId, classId, deviceType, deviceId.

All objects or entities in Opera have an identifier.

The owning organisation, orgId is used to designate the entity responsible for the management of the object or entity.

The classId is used to organise entities and objects in broad categories.

The typeId is used to distinguish different entities in the same class.

Finally, the entity name designated a very precise entity. It can be a serial number, a registration number, or a user assigned unique identifier.

In general, the four identifier parts are grouped together in a `:` separated string.

# Examples of Identifiers

Brussels Airline:Aircraft:A35K:OO-PMA

OTHH:Airway:Taxiway:W05

Airbus:Airliner:A32N:Airbus A320 Neo

OTHH:Airport::Hamad International Airport (please note no `typeId`.)

QAS:GSE:fuel-hydrant:FU04