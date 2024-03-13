
An Identity is the base class for named entity in the Emitpy application.
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

# Notes about Identifier

The idea about the above proposed scheme is that:

The first part, the **Organisation Identifier** determine the entity responsible for the device. It assumes the organisation will also take responsibility of naming devices with the remaining 3 fields.

The **Class of Device** assumes a broad category of device classification, probably a functional typing of the device.

The **Type of the Device** allows for different devices in this functional class: different devices, or models.

Finally, the **Device Identifier** can simply be a serial number, a registration, or any other identifier that uniquely point at this device.

In our context, here are a few examples of each identity part.

- Organisation: Airport, Handler, airport services, aircraft manufacturer
- Class: Vehicle type like aircraft, GSE, etc.
- Type: Aircraft ICAO type, GSE vehicle type (like tow-bar-A32X)
- Name: Aircraft or vehicle registration or serial number


## Technical Note

Often, all four identifier are concatenated into a single, `:` separated list.

`Airport:Ground Handling:Catering:CAT002`

> [!NOTE]
> Try to avoid using `:` in organisation, class, type and device identifier fields.

You are welcomed to use another separator (let us say `|`) inside the above fields.

For example

`HamadIntl|QAS:GSE|Fuel:Hydrant:FU007`

