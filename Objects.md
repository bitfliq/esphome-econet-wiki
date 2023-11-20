# Objects

See <https://github.com/esphome-econet/econet-docs/blob/main/protocol-documentation/Rheem%20BACnet%20Specification.pdf> for a known BACnet object list.

Depending on the object type you can use the following components:

Object type | econet component
----------- | ---------
Analog      | `sensor`
Character String | `text_sensor`
Binary      | `sensor` to get 0 or 1, `text_sensor` to get 'Off' or 'On', `switch` if access is R/W
Multi-State | `sensor` to get enum index, `text_sensor` to get the enum text, `number` or `select` if access is R/W
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

select:
  - platform: econet
    name: "WHTRCNFG select"
    enum_datapoint: WHTRCNFG
    options:
      0: "Off"
      1: "Eco Mode"
      2: "Heat Pump"
      3: "High Demand"
      4: "Electric"
      5: "Vacation"
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

## Water Heater

The following list was obtained with:
```bash
curl https://upgrade.rheemcert.com/RH-WIFI-02-01-25.bin | strings -n 8 | grep -E '^[_A-Z0-9]
{8}$' | sort -u > water_heater_objects.txt
```

Object | Included | Description
------ | -------- | -----------
8FAFJFSF
8FIF2FSF
ACFAILCT
ALARMH01
ALARMH02
ALARMH03
ALARMH04
ALARMH05
ALARMH06
ALARMH07
ALARMH08
ALARMH09
ALARMH10
ALARMH11
ALARMH12
ALARMH13
ALARMH14
ALARMH15
ALARMH16
ALARMH17
ALARMH18
ALARMH19
ALARMH20
ALARMH21
ALARMH22
ALARMH23
ALARMH24
ALARMH25
ALARMNUM
ALARM_01
ALARM_03
ALARM_04
ALARM_05
ALARM_06
ALARM_07
ALARM_08
ALARM_09
ALARM_10
ALARM_11
ALARM_12
ALARM_13
ALARM_14
ALARM_15
ALARM_16
ALARM_17
ALARM_18
ALARM_19
ALARM_20
ALARM_BC
ALRMALRT
APBATTMO
APIRQDTE
APIRQSRV
API_SRVR
APSNDNAK
AP_RSPCT
AUTH_HDR
AWFLFAIL
AWMACADR
BADLNGTH
BADOTHER
BIOS_CRC
BIOS_SIG
BLSTRING
BOOT_CRC
CFCOMFST
CFIDSTRT
CF_FILE1
CF_SIZE1
CIDJHH3F
CLEAR_AP
CLI_HALT
CLNTSRVR
CLOUDTMR
CNAPSSID
CNCONFIG
CNLANTYP
CNPSSWRD
CN_BSSID
CN_CHANL
CONNPREV
DEBUG_AP
DFL_ENAB
EE_WRITE
ENSRVSEC
ENSRVTMO
FAIL2QCT
FHCICJFK
FLASHERA
FL_FSGEN
FORCERCV
FTFS_CRC
FWGENNUM
FWUPGFLG
GD25Q16B
GD25Q16C
GD25Q32C
GIGJIH3F
HFIF2FSF
HRSLOHTR
HRSUPHTR
INSTANCE
JHCIDJ3F
LAST_ACK
LMATIMER
LMBRDMIN
LMBRTIMR
LMCONNEC
LMTIMOUT
LOHTRTMP
MAINSCNT
MAIN_CNT
MARATHON
MAXONOFF
MAXONTIM
MDEV_DMA
MDEV_RTC
MDEV_WDT
MYENMSGS
PFCFDLAY
PRGMWCRC
PRGM_CRC
PRODLOCA
PRODMODN
PRODSERN
PS_ENTER
RECONDLY
RESETDLY
RTRY_LIM
RXI0_CNT
SAFEHILM
SAFELOLM
SCONTIME
SECCOUNT
SERIAL_N
SHUTDOWN
STARTUPR
SVRBSYCT
SVRNAKCT
SVWRTCNT
SW_VERSN
SYN_RCVD
SYN_SENT
TSTALARM
UAPDNTMO
UAPTMREN
UAP_INIT
UHVIVJ3F
UPHTRTMP
VACADAYS
VACALEFT
VACASAVE
VACATIME
VACATION
VACA_NET
W25Q16CL
W25Q32BV
W25Q64CV
WCONTIME
WFFW_CRC
WFGTWYAD
WFIPADDR
WFSECMOD
WHTRCNFG
WHTRCTRL
WHTRENAB
WHTRMODE
WHTRSETP
WLSTATUS
WOLANTYP
WOSCURTY
WO_CHANL
WSTIMOUT
WSTMODEF
WS_CLOSE
