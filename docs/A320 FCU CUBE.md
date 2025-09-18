# A320 FCU CUBE Protocol

USB Information:

- VID: 0xA316
- PID: 0xC787

## Uplink Data

The device send to the computer.


| Name                        | Note                            | Mask | Byte[] | Bit[] | Example |
|-----------------------------|---------------------------------|------|:------:|:-----:|:-------:|
| Head                        | Constant: 0xF2                  |      |   0    |   -   |  0xF2   |
| Head                        | Constant: 0xE1                  |      |   1    |   -   |  0xE1   |
| Head                        | Constant: 0x03                  |      |   2    |   -   |  0x03   |
| Data Type Total             | Has 2 Data Type                 |      |   3    |   -   |  0x02   |
| Data Type                   | Bit Type                        |      |   4    |   -   |  0x01   |
| Data Length                 | Following data occupies 3 Bytes |      |   5    |   -   |  0x03   |
| SPD MACH Switch             | Press:1, Release: 0             | 0x01 |   6    |   0   |    1    |
| SPD Knob Push               | Push: 1, Release: 0             | 0x02 |   6    |   1   |    1    |
| SPD Knob Pull               | Pull: 1, Release: 0             | 0x04 |   6    |   2   |    1    |
| HDG TRK Switch              | Press: 1, Release: 0            | 0x08 |   6    |   3   |    1    |
| HDG Knob Push               | Push: 1, Release: 0             | 0x10 |   6    |   4   |    1    |
| HDG Knob Pull               | Pull: 1, Release: 0             | 0x20 |   6    |   5   |    1    |
| ALT 100                     | Pointing: 1, Non-pointing: 0    | 0x40 |   6    |   6   |    1    |
| ALT 1000                    | Pointing: 1, Non-pointing: 0    | 0x80 |   6    |   7   |    1    |
| ALT Knob Push               | Push: 1, Release: 0             | 0x01 |   7    |   0   |    1    |
| ALT Knob Pull               | Pull: 1, Release: 0             | 0x02 |   7    |   1   |    1    |
| VS Knob Push                | Push: 1, Release: 0             | 0x04 |   7    |   2   |    1    |
| VS Knob Pull                | Pull: 1, Release: 0             | 0x08 |   7    |   3   |    1    |
| METRIC ALT                  | Press: 1, Release: 0            | 0x10 |   7    |   4   |    1    |
| AP1                         | Press: 1, Release: 0            | 0x20 |   7    |   5   |    1    |
| AP2                         | Press: 1, Release: 0            | 0x40 |   7    |   6   |    1    |
| A/THR                       | Press: 1, Release: 0            | 0x80 |   7    |   7   |    1    |
| LOC                         | Press: 1, Release: 0            | 0x01 |   8    |   0   |    1    |
| EXPED                       | Press: 1, Release: 0            | 0x02 |   8    |   1   |    1    |
| APPR                        | Press: 1, Release: 0            | 0x04 |   8    |   2   |    1    |
| (Reserve)                   | -                               | -    |   8    |   3   |    0    |
| (Reserve)                   | -                               | -    |   8    |   4   |    0    |
| (Reserve)                   | -                               | -    |   8    |   5   |    0    |
| (Reserve)                   | -                               | -    |   8    |   6   |    0    |
| (Reserve)                   | -                               | -    |   8    |   7   |    0    |
| Data Type                   | Single Byte Type                | -    |   9    |   -   |  0x02   |
| Data Length                 | Following data occupies 6 Bytes | -    |   10   |   -   |  0x06   |
| SPD Knob Rotate             | 0x00~0xFF  in Two's Complement  | -    |   11   |   -   |    0    |
| HDG Knob Rotate             | 0x00~0xFF  in Two's Complement  | -    |   12   |   -   |    0    |
| ALT Knob Rotate             | 0x00~0xFF  in Two's Complement  | -    |   13   |   -   |    0    |
| VS Knob Rotate              | 0x00~0xFF  in Two's Complement  | -    |   14   |   -   |    0    |
| Background Light Brightness | 0x00(Minium)~0xFF(Maximum)      | -    |   15   |   -   |  0xFF   |
| LCD Light Brightness        | 0x00(Minium)~0xFF(Maximum)      | -    |   16   |   -   |  0xFF   |

**About Knob Rotate Definition:**
Signed values determine rotation direction, with the magnitude representing the rotating count.
So that, this value is in Two's Complement.

**About Light Brightness:**
Those value is controlled by two rotary under the FCU CUBE.

## Downlink Data

The computer send to the device.

| Name                        | Note                               | Mask | Byte[] | Bit[] | Example |
|-----------------------------|------------------------------------|------|:------:|:-----:|:-------:|
| Head                        | Constant: 0xF2                     |      |   0    |   -   |  0xF2   |
| Head                        | Constant: 0xE1                     |      |   1    |   -   |  0xE1   |
| Head                        | Constant: 0x03                     |      |   2    |   -   |  0x03   |
| Data Type Total             | Has 3 Data Type                    |      |   3    |   -   |  0x02   |
| Data Type                   | Bit Type                           |      |   4    |   -   |  0x01   |
| Data Length                 | Following data occupies 3 Bytes    |      |   5    |   -   |  0x03   |
| LOC Signal                  | On:1, Off: 0                       | 0x01 |   6    |   0   |    1    |
| AP1 Signal                  | On:1, Off: 0                       | 0x02 |   6    |   1   |    1    |
| AP2 Signal                  | On:1, Off: 0                       | 0x04 |   6    |   2   |    1    |
| A/THR  Signal               | On:1, Off: 0                       | 0x08 |   6    |   3   |    1    |
| EXPED Signal                | On:1, Off: 0                       | 0x10 |   6    |   4   |    1    |
| APPR Signal                 | On:1, Off: 0                       | 0x20 |   6    |   5   |    1    |
| SPD Managed                 | Circle Point, Active:1, Inactive:0 | 0x40 |   6    |   6   |    1    |
| SPD Dashed                  | Active:1, Inactive:0               | 0x80 |   6    |   7   |    1    |
| HDG Managed                 | Circle Point, Active:1, Inactive:0 | 0x01 |   7    |   0   |    1    |
| HDG Dashed                  | Active:1, Inactive:0               | 0x02 |   7    |   1   |    1    |
| ALT Managed                 | Active:1, Inactive:0               | 0x04 |   7    |   2   |    1    |
| VS Dashed                   | Active:1, Inactive:0               | 0x08 |   7    |   3   |    1    |
| SPD MACH Mode               | SPD:0, MACH:1                      | 0x10 |   7    |   4   |    1    |
| HDG V/S Mode                | HDG V/S:0, TRK FPA:1               | 0x20 |   7    |   5   |    1    |
| Test Mode                   | Turn On All Light And LCD          | 0x40 |   7    |   6   |    1    |
| (Reserve)                   | -                                  | 0x80 |   7    |   7   |    0    |
| Power                       | On:1,Off:0                         | 0x01 |   8    |   0   |    1    |
| (Reserve)                   |                                    | 0x02 |   8    |   1   |    1    |
| (Reserve)                   |                                    | 0x04 |   8    |   2   |    1    |
| (Reserve)                   |                                    | -    |   8    |   3   |    0    |
| (Reserve)                   |                                    | -    |   8    |   4   |    0    |
| (Reserve)                   |                                    | -    |   8    |   5   |    0    |
| (Reserve)  (Reserve)        |                                    | -    |   8    |   6   |    0    |
| (Reserve)                   |                                    | -    |   8    |   7   |    0    |
| Data Type                   | Single Byte Type                   | -    |   9    |   -   |  0x02   |
| Data Length                 | Following data occupies 2 Bytes    | -    |   10   |   -   |  0x02   |
| Background Light Brightness | 0x00(Minimum)-0xFF(Maximum)        | -    |   11   |   -   |    0    |
| LCD Brightness              | 0x00(Minimum)-0xFF(Maximum)        | -    |   12   |   -   |    0    |
| Data Type                   | Double Byte Type                   | -    |   13   |   -   |    0    |
| Data Length                 | Following data occupies 8 Bytes    | -    |   14   |   -   |  0x08   |
| SPD Number                  | High 8 bit of Uint16               | -    |   15   |   -   |  0x00   |
| SPD Number                  | Low 8 bit of Uint16                | -    |   16   |   -   |  0x00   |
| HDG Number                  | High 8 bit of Uint16               | -    |   17   |   -   |  0x00   |
| HDG Number                  | Low 8 bit of Uint16                | -    |   18   |   -   |  0x00   |
| ALT Number                  | High 8 bit of Uint16               | -    |   19   |   -   |  0x00   |
| ALT Number                  | Low 8 bit of Uint16                | -    |   20   |   -   |  0x00   |
| V/S Number                  | High 8 bit of Uint16               | -    |   21   |   -   |  0x00   |
| V/S Number                  | Low 8 bit of Uint16                | -    |   22   |   -   |  0x00   |

**About Power:**
To make any light turn on, You must set Power=1.