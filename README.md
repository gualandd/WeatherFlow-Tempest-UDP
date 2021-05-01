# WeatherFlow - Tempest UDP & API Integration
UDP & Rest API integration with NodeRED for Home Assistant

This is a Node-Red flow that expose full metrics to MQTT only; no more direct exposure to Home Assistant due to resource demand of the HACS companion and to be usable for all.

The flow expose all the UDP Metrics & Data available on port 50222 plus some metrics from the Rest API url: for the correct run of the Rest API
is mandatory to insert in injection nodes the Tempest API and the Station ID.

The derived metrics are calculated & tested with the most recents formulas.
All entities created have the "tempest_" suffix.

********************************
Changelog 01/05/2021:

Removed the direct Home Assistant Exposure: now You have to create MQTT entities in Home Assistant from the configuration.yaml: the flow create a "Tempest_PWS" main topic that is nested with all the available data;

Removed Lightning Strike Distance & Date because no more available on API;

Added filtering function in Rain Ammount & Time due to possible false readings from Rest API: if rain is less than 0.5mm is filtered to 0mm ammount and 0min rain time otherwise actual data is published.
Added filtering function in Lightning detection to avoid false alarms: in lightning total day number is less than 5 is filtered to 0, otherwise actual number is published.

Partial rebuild of the flow to avoid problems with Node-Red Join node.
********************************

EXPOSED UDP INFO (sensor):
- Hub s/n
- Hub Firmware
- Hub Rssi
- Tempest s/n
- Tempest Firmware
- Tempest Rssi
- IP Address

EXPOSED UDP METRICS (sensor):
- UV Index + Description (attribute)
- Solar Radiation (W/m^2)
- Illuminance (Lux)
- Station Pressure (mbar)
- Wind Gust (km/h)
- Temperature (°C)
- Battery (V)
- Precipitation Type (converted in Description)
- Humidity (%H)
- Wind Speed (km/h)
- Wind Speed RealTime (km/h)
- Wind Lull (km/h)
- Wind Direction (deg)
- Wind Direction RealTime (deg)

EXPOSED UDP SENSORS STATUS (binary.sensor):
- Lightning Failed
- Light/UV Failed
- Rain Failed
- Pressure Failed
- Temperature Failed
- Humidity Failed
- Wind Failed
- Lightning Disturber
- Lightning Noise

DERIVATED METRICS (sensor):
- Beaufort Index + Description (attribute)
- Heat Index + Description (attribute)
- Dew Point
- Thom Index + Description (attribute)
- Humidex + Description (attribute)
- Wind Chill (New Formula) + Description (attribute)
- Battery Percentage (%)
- Wind Cardinals
- Wind Cardinals RealTime
- Charging Status (approx.)

REST API METRICS & INFOS (sensor):
- Latitude
- Longitute
- Elevation (m)
- Station Name
- Public Station Name
- Station ID
- Total Today Precip (mm)
- Total Today Precip Time (min)
- Pressure Tendence
- Air Density
- Sea Level Pressure
- Wet Bulb Temperature
- Delta T
- Lightning Strike Count + Last 1hr & Last 3hr attributes

Descriptions are in Italian, but are easy to translate.

Enjoy!
