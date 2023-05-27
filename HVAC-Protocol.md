## Addresses
| Address | Description |
| :---: |:---: | 
| `0x340` | Wifi Module |
| `Ox380` | Thermostat|
| `Ox3c0` | Unknown for now |
| `Ox400` | Unknown for now |

## Fan Modes
| Mode Name | Float # | Description |
| :---: |:---: | :---: |
| `Auto` | 0 | Off |
| `Low` | 1 | Low |
| `Mediun.Lo` | 2 | Medium Low |
| `Medium` | 3 | Medium|
| `Medium.Hi` | 4 | Medium-High |
| `High` | 5 | High |

## Fan Mode Commands
| Command | Type | Value | Description |
| :---: |:---: | :---: | :---: | 
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 00 00 00 00` | Float | 0 | Auto |
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 3F 80 00 00` | Float | 1 | Low |
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 40 00 00 00` | Float | 2 | Medium.Lo |
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 40 40 00 00` | Float | 3 | Medium |
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 40 80 00 00` | Float | 4 | Medium.Hi  |
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 40 A0 00 00` | Float | 5 | High |


## Thermostat Request Data
| Name | Description |
| :---: | :---: |
| `AUTOMODE` |  |
| `AWAYMODE` |  | Whether the thermostat is in away mod|
| `COOLSETP` |  Cooling Set Point|
| `DEADBAND` |  |
| `FURNGFAN` |  |
| `HEATSETP` |  Heat Set Point |
| `HVACMODE` | Running State (i.e. Low Cool) |
| `HW_G_FAN` |  |
| `RELH700` |  Relative Humidity |
| `SPT_STAT` |  Current temperature|
| `STATMODE` |  |
| `STATNFAN` |  | 
| `STAT_FAN` |  |
| `VACSTATE` |  Vacation state |


<details>
  <summary>Raw Data Request</summary>
  
## Command 30 0x340 to 0x380
02.01.00.00.41.55.54.4F.4D.4F.44.45.00.00.41.57.41.59.4D.4F.44.45.00.00.43.4F.4F.4C.53.45.54.50.00.00.44.45.41.44.42.41.4E.44.00.00.46.55.52.4E.47.46.41.4E.00.00.48.45.41.54.53.45.54.50.00.00.48.56.41.43.4D.4F.44.45.00.00.48.57.5F.47.5F.46.41.4E.00.00.52.45.4C.48.37.30.30.35.00.00.53.50.54.00.00.00.00.00.00.00.53.50.54.5F.53.54.41.54.00.00.53.54.41.54.4D.4F.44.45.00.00.53.54.41.54.4E.46.41.4E.00.00.53.54.41.54.5F.46.41.4E.00.00.56.41.43.53.54.41.54.45 

</details>


## Thermostat Response to Data Request
| Request | Response | Type | Value |
| :---: | :---: |:---: | :---: |
|`AUTOMODE` | `0C.82.00.00.01.07.43.6F.6F.6C.69.6E.67.01.15` | Enumerated Text | Off |
|`AWAYMODE` | `` | | ? |
|`COOLSETP` | `07.80.00.00.42.80.00.0` | Float | 64 |
|`DEADBAND` | `07.80.00.00.40.00.00.00` | Floating | 2 |
|`FURNGFAN` | `0E.82.00.00.00.09.4F.66.66.20.20.20.20.20.20` | Enumerated Text | Off |
|`HEATSETP` | `07.80.00.00.42.74.00.00` | Float | 61 |
|`HVACMODE` | `0F.82.00.00.02.0A.4C.6F.77.20.43.6F.6F.6C.20.00` | Enumerated Text | Low Cool |
|`HW_G_FAN` | `08.82.00.00.00.03.4F.66.66` | Enumerated Text | Off |
|`RELH7005` | `07.80.00.00.42.39.3D.BF` | Float | 46.3103 |
|`SPT_STAT` | `07.80.00.00.42.80.52.4F` | Float | 64.1608 |
|`STATMODE` | `13.82.00.00.01.0E.43.6F.6F.6C.69.6E.67.20.20.20.20.20.20.20` | Enumerated Text | Cooling |
|`STATNFAN` | `0B.82.00.00.00.06.41.75.74.6F.20.20` | Enumerated Text | Auto |
|`STAT_FAN` | `0B.82.00.00.00.06.4F.66.66.20.20.20` | Enumerated Text | Off |
|`VACSTATE` | `08.82.00.00.00.03.4E.6F.20` | Enumerated Text | ? |

<details>
  <summary>Raw Data Request</summary>
  
## Command 6 0x380 to 0x340
0C.82.00.00.01.07.43.6F.6F.6C.69.6E.67.01.15.07.80.00.00.42.80.00.00.07.80.00.00.40.00.00.00.0E.82.00.00.00.09.4F.66.66.20.20.20.20.20.20.07.80.00.00.42.74.00.00.0F.82.00.00.02.0A.4C.6F.77.20.43.6F.6F.6C.20.00.08.82.00.00.00.03.4F.66.66.07.80.00.00.42.39.3D.BF.07.80.00.00.42.80.52.4F.07.80.00.00.42.80.00.00.13.82.00.00.01.0E.43.6F.6F.6C.69.6E.67.20.20.20.20.20.20.20.0B.82.00.00.00.06.41.75.74.6F.20.20.0B.82.00.00.00.06.4F.66.66.20.20.20.08.82.00.00.00.03.4E.6F.20
</details>

## HVAC Modes
| Mode Name | Float # | Description |
| :---: |:---: | :---: |
| `Heating` | 0 | Heat |
| `Cooling` | 1 | AC |
| `Auto` | 2 | Heat/AC |
| `Fan Only` | 3 | Fan |
| `Off` | 4 | Off |

## HVAC Mode Command
| Command | Type | Value | Mode Name |
| :---: |:---: | :---: | :---: |
| `01.01.02.01.00.00.53.54.41.54.4D.4F.44.45.3F.80.00.00` | Float | 1 | Cooling |
| `01.01.02.01.00.00.53.54.41.54.4D.4F.44.45.40.00.00.00` | Float | 2 |  Auto |

## Set Temperature Command
| Command | Type | Value |
| :---: |:---: | :---: |
| `01.01.00.01.00.00.43.4F.4F.4C.53.45.54.50.42.7C.00.00` | Float | 63 |
| `01.01.00.01.00.00.43.4F.4F.4C.53.45.54.50.42.80.00.00` | Float | 64 |

## Thermostat Ack
#### 80 00 03 40 00 80 00 03 80 00 01 00 00 06 01 BD 09