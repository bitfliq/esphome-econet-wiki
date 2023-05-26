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
| Command | Type | Description |
| :---: |:---: | :---: |
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 00 00 00 00` | Float | Auto (0) |
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 3F 80 00 00` | Float | Low (1) |
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 40 00 00 00` | Float | Medium.Lo (2) |
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 40 40 00 00` | Float | Medium (3) |
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 40 80 00 00` | Float | Medium.Hi (4) |
| `01 01 02 01 00 00 53 54 41 54 4E 46 41 4E 40 A0 00 00` | Float | High (5) |