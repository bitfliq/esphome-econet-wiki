Water Heaters expose a power sensor which provides the current power usage of the device; e.g. on Heat Pump Water Heaters this is the "Power" sensor (based on the POWRWATT attribute) and is provided in Watts. To understand actual energy usage of your device, you might want to convert this to [Kilowatt-Hours](https://en.wikipedia.org/wiki/Kilowatt-hour), or kWh, which is what is generally the billed unit of electricity use (at least in the United States).

The Power sensor provides the moment-in-time usage, in Watts, sampled periodically. To convert this to a kWh metric, you need to take the Integral. No need to brush up on your calculus, though: This is easily done in Home Assistant!

To convert this to kWh's via the Home Assistant UI:

* Navigate to `Settings -> Devices & Services -> Helpers` and click the `+ Create Helper` button
* Select `Integration - Riemann sum integral sensor`
* Configure Your New Sensor: 
  * Name your sensor something like "Water Heater Power Usage"
  * Set the Input Sensor to be your Water Heater's Power entity (e.g. `sensor.econet_power`)
  * Select a `Left Riemann Sum` with a `k` prefix and an `Hours` unit

Alternatively, you can create this sensor via your configuration.yaml like so:

```yaml
sensor:
  - platform: integration
    unique_id: water_heater_power_consumption
    name: "Water Heater Power Consumption"
    source: sensor.econet_power
    unit_prefix: k
    unit_time: h
    method: left
```

If desired, you can then use the same `Helper` mechanism to create a `Utility Meter` sensor to give you the daily, weekly, or monthly total power usage of your appliance.

More details can be found here: https://community.home-assistant.io/t/2021-8-new-energy-feature-in-ha-conversion-from-w-to-kwh/328830
