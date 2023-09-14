Emitpy takes into account weather information at the following flight phases:
- Departure airport: Wind speed and direction, precipitations; to select runway orientation and adjust take-off distance.
- En route: Wind at the expected aircraft level; to adjust ground speed and heading.
- Arrival airport: Wind speed and direction, precipitations; to select runway orientation and adjust landing distance.

Weather can be provided from different sources.

# Weather

## Weather at Airports

The API for weather at airport is limited to:
1. Wind speed and direction
2. Amount of precipitations
Weather can be requested at any time (default is now).


For current and historical weather at airport, Emitpy uses METAR reports.
For weather at airport in a close future (less than 24 hours), Emitpy uses TAF reports.

METAR and TAF reports are fetched from NOAA servers.

If a past weather cannot be fetched, the current weather is be used instead, or weather information can be ignored.

Past METAR are fetched from [ogimet](https://www.ogimet.com) archive server, however access is limited.

If weather cannot be determined at an airport, runway orientation (QFU) is randomly selected, and VFR conditions are assumed with no precipitation.

METAR and TAF are cached and never fetched twice.

## En Route Weather

The API for en-route weather limited to:
1. Wind speed and direction at given 4D position (latitude, longitude, altitude, time)
Wind can be requested at any time (default is now).

For current en-route weather, Emitpy uses
- either current GFS prediction for the next flight hours/duration (typically 12, 18, or 24 hours),
- or X-Plane pre-processed weather files (also in GRIB format, predictions at 3 and 6 hours, updated frequently if X-Plane is running.

GFS files are fetched from GFS servers available worldwide.

For past en-route weather, Emitpy uses past GFS files if available. If not available *emitpy* either uses the current GFS file if available or ignore wind during cruise phase.

If en-route weather cannot be fetched, no wind is added to the flight (course=heading, speed=TAS).

Other forecast algorithms can be used for en-route wind estimation. GFS are widely available.

# Flight Time

Depending on the flight time, past or present, it is possible to fetch weather at the following moment.

Emitpy allows to replay a flight that was scheduled in the past at any time. For example, a flight that was originally scheduled Apr. 1rst 2019 at 10am can be played Aug. 6 2023 at 11. Since the flight occurs on Aug. 6th the weather at that time is be fetched.

## Arrivals

### Airports
For Arrivals, weather at departure and arrival airports can be determined from historical or current METAR. If historical METAR is not available, the current METAR is used instead.

### En-Route
For en-route winds, we use the wind predictions that were available at the time of departure, like pilots would have taken into account in their flight plan. The fall back is to use the current forecast.

## Departure

### Airports
For departing airport, we use historical or current METAR.
For arrival airport, for a flight in the past, we use (in order):
- Historical METAR at the time of arrival (exact weather)
- Historical TAF at the time of departure, like pilots would have used
- Current TAF at destination at time of departure
- Current METAR at destination at time of departure
For a flight « now », we use the current TAF at the destination airport.
(Since we mainly deal with large airports, TAF are often available.)
If the TAF is not available at the destination airport, we use the current METAR.

### En-Route
For en-route winds, we use the historical wind predictions that were available at the time of departure for the departure airport, like pilots would have taken into account in their flight planning.
The fall back is to use the current forecast.

# Forecast

For en-route wind forecast, we only use one set of data for simplicity. The time of the prediction is not adjusted as flight progresses.
Depending on the duration of the flight, we try to get the following prediction:
- Flights less that 6 hours: predictions at 3 h (after the scheduled or estimated time of departure)
- Flights more that 6 hours: predictions at 6 hours.
Both forecast at readily available, especially when using X-Plane Real weather files.

Same occurs when trying to estimate TAF predictions to be taken into account at the scheduled or estimated time of arrival at destination airport.

# Weather Engine

The Weather Engine is responsible for providing weather information at airports (historical or current METAR or TAF), and for flight routes.

## Weather Adjustment

There is no adjustment (changes of flight level, heading, etc.) to optimise flights when weather is added. The weather (wind) component is simply added to the flight route, only altering speed and timing information.
