
# Geospatial Data Handling

If you are looking for a "pure python", well, as pure as you can get, for basic geospatial options, please head for `pyturf` ([turfpy](https://turfpy.readthedocs.io/en/latest/)) rather than other GeoJSON and [turf](http://turfjs.org) python packages.
 Pyturf includes GeoJSON helper class and functions that respect the `__geo_interface` specification. Pyturf is very pythonic, use simple pytest, is how any python package should be.
I took me an entire day to switch from geojson/turpy to pyturf.

# Yaml rather than JSON

If possible, Yaml files are so much easier to read. Yaml is a *superset* of JSON, which means that all JSON files are valid Yaml files and can be read and processed by Yaml readers.
I wish GeoJSON be GeoYaml and pyturf accept GeoYaml. This can easily be done thanks to tiny wrappers.