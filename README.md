# WeatherFlow - Tempest UDP & API Integration
UDP & Rest API integration with NodeRED for Home Assistant

This is a Node-Red flow that expose full metrics to Home Assistant; for the correct running of the flow the Node-Red HACS is required for the HA-Entity creation.

The flow expose all the UDP Metrics & Data available on port 50222 plus some metrics from the Rest API url dor a total of 52 entities: for the correct run of the Rest API
is mandatory to insert in injection nodes the Tempest API and the Station ID.
All the available Rest infos are exposed in NR but only few are exposed to HA too, so is possible to expose extra info to HA simply add the relative entity node.
I've inserted a check inside the flow to eliminate the startup error with entities when data flow in injected in ha-entity before the entity is connected to HA:
it checks that all 52 have the green status and then allow the message flow to pass (via a traffic node).
For this reason, if someone will add or delete some entities from the flow is necessary to modify the number inside the funcion node that check the entities status.

The derived metrics are calculated & tested with the most recents formulas.
All entities created have the "tempest_" suffix.

********************************
Changelog 16/01/2021:
Added MQTT publishing: the flow create a "Tempest_PWS" main topic that is nested with all the available data;
Removed Lightning Strike Distance & Date because no more available on API;
Added 4 new sensors from API (Air Density, Sea Level Pressure, Wet Bulb Temp. and Delta T);
Partial rebuild of the flow for avoid that new API metrics make problems.
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
