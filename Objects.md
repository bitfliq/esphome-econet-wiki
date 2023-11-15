# Objects

See <https://github.com/esphome-econet/econet-docs/blob/main/protocol-documentation/Rheem%20BACnet%20Specification.pdf> for a known BACnet object list.

Depending on the object type you can use the following components:

Object type | econet component
----------- | ---------
Analog      | `sensor`
Character String | `text_sensor`
Binary      | `sensor` to get 0 or 1, `text_sensor` to get 'Off' or 'On', `switch` if access is R/W
Multi-State | `sensor` to get enum index, `text_sensor` to get the enum text, `number` if access is R/W
RAW         | `on_datapoint_update`

e.g. for `WHTRCNFG` which is multi-state R/W you can use:

```yaml
sensor:
  - platform: econet
    name: "WHTRCNFG"
    sensor_datapoint: WHTRCNFG

text_sensor:
  - platform: econet
    name: "WHTRCNFG text"
    sensor_datapoint: WHTRCNFG

number:
  - platform: econet
    name: "WHTRCNFG number"
    number_datapoint: WHTRCNFG
    min_value: 0
    max_value: 100
    step: 1
    mode: box
```

e.g. for `DEFAULTS` (be careful using this since it will clear model number and serial number) which is binary R/W you can have a hidden switch and a button that flips it:

```yaml
switch:
  - platform: econet
    id: defaults
    switch_datapoint: DEFAULTS
    request_mod: none
    internal: true

button:
  - platform: template
    name: "Restore program defaults"
    id: restore_program_defaults
    entity_category: "config"
    on_press:
      - switch.turn_on: defaults
      - delay: 1s
      - switch.turn_off: defaults
```

For objects that are RAW, e.g. `AIRHSTAT` you can follow this example:

```yaml
econet:
  on_datapoint_update:
    - sensor_datapoint: AIRHSTAT
      datapoint_type: raw
      then:
        - lambda: |-
            ESP_LOGD("main", "on_datapoint_update %s", format_hex_pretty(x).c_str());
            id(blower_cfm).publish_state((x[16] << 8) + x[17]);

sensor:
  - platform: template
    name: "Air Handler CFM"
    id: blower_cfm
```

You can use `request_mod` to group requests for some objects together. It defaults to 0. Objects with the same `request_mod` will be requested together. This is needed to make sure we get a response especially when requesting large string values. e.g. we can only request up to 2 alarm history objects. Anything more and there is no response. You can use `request_mod: none` if there is no need to request some objects. They will still be updated if another device, e.g. thermostat, requests these objects in the bus.

You can use `request_once: true` for objects that aren't expected to change, e.g. serial number.
