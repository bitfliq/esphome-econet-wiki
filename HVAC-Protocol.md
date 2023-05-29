## Addresses
| Address | Description |
| :---: |:---: | 
| `0x340` | Wifi Module |
| `Ox380` | Thermostat|
| `Ox3c0` | Air handler |
| `Ox400` | Heatpump |

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
| `AWAYMODE` | Whether the thermostat is in away mode |
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
  <summary>Raw Data Response</summary>
  
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

# HVAC Diagnostic Data

## Thermostat request for diagnostic data from air handler

| Name | Description |
| :---: | :---: |
| `AAUX1CFM` |  |
| `AAUX2CFM` |  |
| `AAUX3CFM` | |
| `AAUX4CFM` |  |
| `AIRHSTAT` | |

<details>
  <summary>Raw Data Request</summary>
  
## Command 30 0x380 to 0x3c0 AAUX1CFM to AAUX4CFM
02.01.00.00.41.41.55.58.31.43.46.4D.00.00.41.41.55.58.32.43.46.4D.00.00.41.41.55.58.33.43.46.4D.00.00.41.41.55.58.34.43.46.4D
## Command 30 0x380 to 0x3c0 AIRHSTAT
01.01.00.00.41.49.52.48.53.54.41.54
</details>

## Air handler response

| Request | Response | Type | Value |
| :---: | :---: |:---: | :---: |
|`AAUX1CFM` | `07.80.00.00.44.C8.00.00` | Float | 1600 |
|`AAUX2CFM` | `07.80.00.00.44.C8.00.00` | Float | 1600 |
|`AAUX3CFM` | `07.80.00.00.44.48.00.00` | Float | 800 |
|`AAUX4CFM` | `07.80.00.00.44.16.00.00` | Float | 600 |
|`AIRHSTAT` | `See Raw Data Response` | ? | ? |

<details>
  <summary>Raw Data Response</summary>
  
## Command 6 0x3c0 to 0x380 AAUX1CFM to AAUX4CFM
07.80.00.00.44.C8.00.00.07.80.00.00.44.C8.00.00.07.80.00.00.44.48.00.00.07.80.00.00.44.16.00.00
## Command 6 0x3c0 to 0x380 AIRHSTAT
84.00.00.00.00.00.00.00.00.00.00.DB.01.08.07.00.00.00.00.00.00.00.00.40.06.40.06.00.00.00.00.00.00.00.00.00.00.00.00.00.00.41.43.2D.41.49.52.48.2D.30.30.2D.30.31.2D.31.30.00.42.48.AE.FC.42.55.55.20.C2.20.00.00.00.00.01.00.27.00.00.00.00.00.00.00.75.00.00.00.0A.A2.00.00.09.69.00.00.27.53.00.00.00.5E.00.00.01.DE.00.00.01.6B.00.00.44.F2.08.09.00.1A.82.05.00.00.00.00.00.00.00.00.00.00.00.00.00.00.00.01.01.00.00.42.C0.00.00.41.1B.F0.94.42.6E.87.17.42.47.8A.F2.43.1C.FD.68.00.00.00
</details>

## Thermostat request for diagnostic data from heatpump 

| Name | Description |
| :---: | :---: |
| `ALARM_01` |  |
| `ALARM_01` |  |
| `ALARM_01` | |
| `ALARM_01` |  |
| `LOCKTIMR` | Hold Off Timer |
| `TEMP_OAT` | Outdoor Air Temperature |
| `TEMP_EVP` | Evaporator Temp |
| `ODU_DEFR` | Outdoor Unit xyz?|
| `ODURCS1H` | Low Cool Two Week Hours|
| `ODURCS2H` | High Cool Two Week Hours |
| `ODURHS1H` | Low Heat Two Week Hours |
| `ODURHS2H` | High Heat Two Week Hours |
| `ODURCS1C` | Low Cool Two Week Cycles |
| `ODURCS2C` | High Cool Two Week Cycles |
| `ODURHS1C` | Low Heat Two Week Cycles |
| `ODURHS2C` | High Heat Two Week Cycles |
| `ODULCS1H` | Low Cool Lifetime Hours |
| `ODULCS2H` | High Cool Lifetime Hours |
| `ODULHS1H` | Low Heat Lifetime Hours |
| `ODULHS2H` | High Heat Lifetime Hours |
| `ODULCS1C` | Low Cool Lifetime Cycles |
| `ODULCS2C` | High Cool Lifetime Cycles |
| `ODULHS1C` | Low Heat Lifetime Cycles |
| `ODULHS2C` | High Heat Lifetime Cycles |
| `ODURDEFC` | Defrost Cycles Two Week Hours |
| `ODULDEFC` | Defrost Cycles Lifetime Hours |
| `ODU_DAYS` | |
| `MAXSPEED` | Max RPM? |
| `MIN__RPM` | |
| `CMP_TYPE` | |
| `U__INPUT` | |

<details>
  <summary>Raw Data Request</summary>
  
## Command 30 0x380 to 0x400 ALARM_01 to ALARM_04
02.01.00.00.41.4C.41.52.4D.5F.30.31.00.00.41.4C.41.52.4D.5F.30.32.00.00.41.4C.41.52.4D.5F.30.33.00.00.41.4C.41.52.4D.5F.30.34 
## Command 30 0x380 to 0x400 LOCKTIMR to ODU_DEFR
02.01.00.00.4C.4F.43.4B.54.49.4D.52.00.00.54.45.4D.50.5F.4F.41.54.00.00.54.45.4D.50.5F.45.56.50.00.00.4F.44.55.5F.44.45.46.52
## Command 30 0x380 to 0x400 ODURCS1H to U__INPUT
02.01.00.00.4F.44.55.52.43.53.31.48.00.00.4F.44.55.52.43.53.32.48.00.00.4F.44.55.52.48.53.31.48.00.00.4F.44.55.52.48.53.32.48.00.00.4F.44.55.52.43.53.31.43.00.00.4F.44.55.52.43.53.32.43.00.00.4F.44.55.52.48.53.31.43.00.00.4F.44.55.52.48.53.32.43.00.00.4F.44.55.4C.43.53.31.48.00.00.4F.44.55.4C.43.53.32.48.00.00.4F.44.55.4C.48.53.31.48.00.00.4F.44.55.4C.48.53.32.48.00.00.4F.44.55.4C.43.53.31.43.00.00.4F.44.55.4C.43.53.32.43.00.00.4F.44.55.4C.48.53.31.43.00.00.4F.44.55.4C.48.53.32.43.00.00.4F.44.55.52.44.45.46.43.00.00.4F.44.55.4C.44.45.46.43.00.00.4F.44.55.5F.44.41.59.53.00.00.4D.41.58.53.50.45.45.44.00.00.4D.49.4E.5F.5F.52.50.4D.00.00.43.4D.50.5F.54.59.50.45.00.00.55.5F.5F.49.4E.50.55.54

</details>

## Heatpump response

| Request | Response | Type | Value |
| :---: | :---: |:---: | :---: |
|`ALARM_01` | `See Raw Data Response` | ? | ? |
|`ALARM_02` | `See Raw Data Response` | ? | ? |
|`ALARM_03` | `See Raw Data Response` | ? | ? |
|`ALARM_04` | `See Raw Data Response` | ? | ? |
|`LOCKTIMR` | `07.80.00.00.00.00.00.00` | Float | 0 |
|`TEMP_OAT` | `07.80.00.00.42.83.EE.98` | Float | 65.966 |
|`TEMP_EVP` | `07.80.00.00.42.85.BF.0A` | Float | 66.8731 |
|`ODU_DEFR` | `07.80.00.00.00.00.00.00` | Float | 0 |
|`ODURCS1H` | `07.80.00.00.42.D2.00.00` | Float | 105 |
|`ODURCS2H` | `07.80.00.00.3F.80.00.00` | Float | 1 |
|`ODURHS1H` | `07.80.00.00.40.00.00.00` | Float | 2 |
|`ODURHS2H` | `07.80.00.00.40.00.00.00` | Float | 2 |
|`ODURCS1C` | `07.80.00.00.00.00.00.00` | Float | 0 |
|`ODURCS2C` | `07.80.00.00.40.40.00.00` | Float | 3 |
|`ODURHS1C` | `07.80.00.00.41.60.00.00 ` | Float | 14 |
|`ODURHS2C` | `07.80.00.00.40.E0.00.00` | Float | 7 |
|`ODULCS1H` | `07.80.00.00.45.C8.F0.00` | Float | 6430 |
|`ODULCS2H` | `07.80.00.00.44.56.00.00` | Float | 856 |
|`ODULHS1H` | `07.80.00.00.45.6C.50.00` | Float | 3781 |
|`ODULHS2H` | `07.80.00.00.45.A6.58.00` | Float | 5323 |
|`ODULCS1C` | `07.80.00.00.45.7F.70.00` | Float | 4087 |
|`ODULCS2C` | `07.80.00.00.44.59.00.00` | Float | 868 |
|`ODULHS1C` | `07.80.00.00.46.32.80.00` | Float | 11424 |
|`ODULHS2C` | `07.80.00.00.45.C5.D0.00` | Float | 6330 |
|`ODURDEFC` | `07.80.00.00.3F.80.00.00` | Float | 1 |
|`ODULDEFC` | `07.80.00.00.44.8F.20.00` | Float | 1145 |
|`ODU_DAYS` | `07.80.00.00.45.0F.D0.00` | Float | 2301 |
|`MAXSPEED` | `07.80.00.00.45.2F.00.00` | Float | 2800 |
|`MIN__RPM` | `07.80.00.00.44.C8.00.00` | Float | 1600 |
|`CMP_TYPE` | `07.80.00.00.3F.80.00.00` | Float | 1 |
|`U__INPUT` | `08.82.00.00.01.03.59.65.73` | ? | ? |


<details>
  <summary>Raw Data Response</summary>
  
## Command 6 0x400 to 0x380 ALARM_01 to ALARM_04
34.81.00.00.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.00.34.81.00.00.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.00.34.81.00.00.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.00.34.81.00.00.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.20.00 
## Command 6 0x400 to 0x380 LOCKTIMR to ODU_DEFR
07.80.00.00.00.00.00.00.07.80.00.00.42.83.EE.98.07.80.00.00.42.85.BF.0A.07.80.00.00.00.00.00.00
## Command 6 0x400 to 0x380
07.80.00.00.42.D2.00.00.07.80.00.00.3F.80.00.00.07.80.00.00.40.00.00.00.07.80.00.00.40.00.00.00.07.80.00.00.41.E8.00.00.07.80.00.00.40.40.00.00.07.80.00.00.41.60.00.00.07.80.00.00.40.E0.00.00.07.80.00.00.45.C8.F0.00.07.80.00.00.44.56.00.00.07.80.00.00.45.6C.50.00.07.80.00.00.45.A6.58.00.07.80.00.00.45.7F.70.00.07.80.00.00.44.59.00.00.07.80.00.00.46.32.80.00.07.80.00.00.45.C5.D0.00.07.80.00.00.3F.80.00.00.07.80.00.00.44.8F.20.00.07.80.00.00.45.0F.D0.00.07.80.00.00.45.2F.00.00.07.80.00.00.44.C8.00.00.07.80.00.00.3F.80.00.00.08.82.00.00.01.03.59.65.73 
</details>