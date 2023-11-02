


# Geospatial Data Handling

If you are looking for a "pure python", well, as pure as you can get, for basic geospatial options, please head for pyturf rather than other geojson and turfpy packages.

Pyturf includes geojson helper class and functions that can easily replace geojson's. The latter has really issues and errors that you will pay over time. turfpy also lacks precise documentation and you end up reading codes to understand. Please walk away of geojson, I do not understand why such package has so many stars. 

Pyturf is very pythonic, use simple pytest, is how any python package should be.
I took me an entire day to switch from geojson/turpy to pyturf.

# Yaml rather than Json
If possible, Yaml files are so much easier to read. Yaml is a *superset* of json, which means that all Json files are valid Yaml files and can be read and processed by Yaml readers.
I wish GeoJSON be GeoYaml and pyturf accept GeoYaml. This can easily be done thanks to tiny wrappers.