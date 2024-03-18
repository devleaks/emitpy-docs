Emitpy uses GeoJSON format for representation, use, input and output of geographic entities. GeoJSON Features in particular carry both geographic information and properties associated with it in a human readable format. (geoyaml would be ideal to get rid of too many quotes.)
Python package [GeoJSON](https://github.com/jazzband/python-geojson) is used in numerous libraries. However it is feature limited and exhibit some problem (e.g. [162](https://github.com/jazzband/geojson/issues/162), [178](https://github.com/jazzband/geojson/issues/178)) that prevent its use in emitpy.

To circumvent this, emitpy uses a `FeatureWithProps` subclass of the above GeoJSON Feature that offert necessary GeoJSON features for external libraries, while maintaing a high level of usability for the emitpy development. FeatureWithProps is the base entity for all emitpy geolocalised features.

Properties attached by emitpy to FeatureWithProps are stored in a dictionary. Property names are listed in the FEATPROP enumeration. Convenient setter and getter functions are provided for properties. Property values can be dictionaries, leading to a structured list of properties. Ultimately, this hierarchy of properties can be flattened to a simpler list of (name, scalar value) pair.

## Feature Colors

A Feature is fitted with two special colors a that can be later used to highlight them on a map. Colors can also be used through lookup tables to map other attributes (icons, for example: red=fire-truck icon).

### Subject Color
The `subject-color` is linked to the emitting vehicle. It can be linked to the type of vehicle (aircraft, fuel, pushback truck, emergency…), its function and model (ambulance, police, fire…)

### Movement Color
The `move-color` is related to the part of the movement of the emitting vehicle. For an aircraft, it can be linked to the flight phase for example (take-off, climb, cruise, decend…).
 