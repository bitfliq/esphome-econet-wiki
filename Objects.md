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
curl https://upgrade.rheemcert.com/RH-WIFI-02-01-25.bin | strings -n 8 | grep -E '^[_A-Z0-9]{8}$' | sort -u
```
and tested on a HPWH:

```
ALARMH01 : ()
ALARMH20 : ()
ALARMNUM : 65.000000
ALARM_01 : ()
ALARM_20 : ()
ALARM_BC : 0 (No)
ALRMALRT : 0.000000
API_SRVR : (http://api.rheemcert.com:80)
AWMACADR : (CC-XX-XX-XX-XX-XX)
BOOT_CRC : 14115.000000
CNAPSSID : (guest)
CNCONFIG : (1)
CNPSSWRD : (XX)
DEFAULTS : 0 (No)
EE_WRITE : 94.000000
FTFS_CRC : 7267.000000
HRSLOHTR : 0.000000
HRSUPHTR : 0.000000
INSTANCE : 1.000000
LOHTRTMP : 121.259674
MAIN_CNT : 1648.000000
MAXONOFF : 3600.000000
MAXONTIM : 43200.000000
PRGMWCRC : 55562.000000
PRGM_CRC : 29486.000000
PRODLOCA : ()
PRODMODN : ()
PRODSERN : ()
SAFEHILM : 152.000000
SAFELOLM : 103.000000
SECCOUNT : 486523.000000
SHUTDOWN : 0 (No)
SW_VERSN : (WH-HPW5-H6-01-04)
UPHTRTMP : 125.704582
VACADAYS : 7.000000
VACALEFT : 0.000000
VACASAVE : 1.000000
VACATIME : 10000.000000
VACATION : 0 (No)
VACA_NET : 0 (Off)
WFFW_CRC : 42599.000000
WFGTWYAD : ()
WFIPADDR : ()
WHTRCNFG : 1 (Energy Saver)
WHTRCTRL : 1 (Energy Saver)
WHTRENAB : 1 (Enabled)
WHTRMODE : 4 (Off: No Demand)
WHTRSETP : 120.000000
WLSTATUS : (Ready To Connect)
```

Additional strings of 8 characters found in the firmware that didn't return any data:

```
8FAFJFSF
8FIF2FSF
ACFAILCT
APBATTMO
APIRQDTE
APIRQSRV
APSNDNAK
AP_RSPCT
AUTH_HDR
AWFLFAIL
BADLNGTH
BADOTHER
BIOS_CRC
BIOS_SIG
BLSTRING
CFCOMFST
CFIDSTRT
CF_FILE1
CF_SIZE1
CIDJHH3F
CLEAR_AP
CLI_HALT
CLNTSRVR
CLOUDTMR
CNLANTYP
CN_BSSID
CN_CHANL
CONNPREV
DEBUG_AP
DFL_ENAB
ENSRVSEC
ENSRVTMO
FAIL2QCT
FHCICJFK
FLASHERA
FL_FSGEN
FORCERCV
FWGENNUM
FWUPGFLG
GD25Q16B
GD25Q16C
GD25Q32C
GIGJIH3F
HFIF2FSF
JHCIDJ3F
LAST_ACK
LMATIMER
LMBRDMIN
LMBRTIMR
LMCONNEC
LMTIMOUT
MAINSCNT
MARATHON
MDEV_DMA
MDEV_RTC
MDEV_WDT
MYENMSGS
PFCFDLAY
PS_ENTER
RECONDLY
RESETDLY
RTRY_LIM
RXI0_CNT
SCONTIME
SERIAL_N
STARTUPR
SVRBSYCT
SVRNAKCT
SVWRTCNT
SYN_RCVD
SYN_SENT
TSTALARM
UAPDNTMO
UAPTMREN
UAP_INIT
UHVIVJ3F
W25Q16CL
W25Q32BV
W25Q64CV
WCONTIME
WFSECMOD
WOLANTYP
WOSCURTY
WO_CHANL
WSTIMOUT
WSTMODEF
WS_CLOSE
```
