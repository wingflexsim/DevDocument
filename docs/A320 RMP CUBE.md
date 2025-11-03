# A320 OVHD CUBE Protocol

USB Information:

- VID: 0xA616
- PID: 0x5750

## Uplink Data

The device send to the computer.

| Name                             | Note                            | Mask | Byte[] | Bit[] | Example |
|----------------------------------|---------------------------------|------|:------:|:-----:|:-------:|
| Head                             | Constant: 0xF2                  |      |   0    |   -   |  0xF2   |
| Head                             | Constant: 0xE1                  |      |   1    |   -   |  0xE1   |
| Head                             | Constant: 0x06                  |      |   2    |   -   |  0x06   |
| Data Type Total                  | Has 2 Data Type                 |      |   3    |   -   |  0x02   |
| Data Type                        | Bit Type                        |      |   4    |   -   |  0x01   |
| Data Length                      | Following data occupies 4 Bytes |      |   5    |   -   |  0x04   |
| Transfer Key                     | Press:1, Release: 0             | 0x01 |   6    |   0   |    0    |
| VHF1 Key                         | Press: 1, Release: 0            | 0x02 |   6    |   1   |    0    |
| VHF2 Key                         | Press: 1, Release: 0            | 0x04 |   6    |   2   |    0    |
| VHF3 Key                         | Press: 1, Release: 0            | 0x08 |   6    |   3   |    0    |
| LOAD Key                         | Press: 1, Release: 0            | 0x10 |   6    |   4   |    0    |
| HF1 Key                          | Press: 1, Release: 0            | 0x20 |   6    |   5   |    0    |
| HF2 Key                          | Press: 1, Release: 0            | 0x40 |   6    |   6   |    0    |
| ATC Key                          | Press: 1, Release: 0            | 0x80 |   6    |   7   |    0    |
| NAV Key                          | Push: 1, Release: 0             | 0x01 |   7    |   0   |    0    |
| VOR Key                          | Pull: 1, Release: 0             | 0x02 |   7    |   1   |    0    |
| ILS Key                          | Push: 1, Release: 0             | 0x04 |   7    |   2   |    0    |
| GLS Key                          | Pull: 1, Release: 0             | 0x08 |   7    |   3   |    0    |
| MLS Key                          | Press: 1, Release: 0            | 0x10 |   7    |   4   |    0    |
| ADF Key                          | Press: 1, Release: 0            | 0x20 |   7    |   5   |    0    |
| Encoder Key - IDENT              | Press: 1, Release: 0            | 0x40 |   7    |   6   |    0    |
| Power On                         | Press: 1, Release: 0            | 0x80 |   7    |   7   |    1    |
| Power Off                        | Press: 1, Release: 0            | 0x01 |   8    |   0   |    0    |
| ATC MSG Key                      | Press: 1, Release: 0            | 0x02 |   8    |   1   |    0    |
| AUTO LAND Key                    | Press: 1, Release: 0            | 0x04 |   8    |   2   |    0    |
| Mode Selector - STBY             | Pointing: 1, Non-pointing: 0    | 0x08 |   8    |   3   |    1    |
| Mode Selector - ON               | Pointing: 1, Non-pointing: 0    | 0x10 |   8    |   4   |    0    |
| Mode Selector - AUTO             | Pointing: 1, Non-pointing: 0    | 0x20 |   8    |   5   |    0    |
| TCAS Mode - STBY                 | Pointing: 1, Non-pointing: 0    | 0x40 |   8    |   6   |    1    |
| TCAS Mode - TA                   | Pointing: 1, Non-pointing: 0    | 0x80 |   8    |   7   |    0    |
| TCAS Mode - TA/RA                | Pointing: 1, Non-pointing: 0    | 0x01 |   9    |   0   |    0    |
| (Reserve)                        | -                               | -    |   9    |   1   |    0    |
| (Reserve)                        | -                               | -    |   9    |   2   |    0    |
| (Reserve)                        | -                               | -    |   9    |   3   |    0    |
| (Reserve)                        | -                               | -    |   9    |   4   |    0    |
| (Reserve)                        | -                               | -    |   9    |   5   |    0    |
| (Reserve)                        | -                               | -    |   9    |   6   |    0    |
| (Reserve)                        | -                               | -    |   9    |   7   |    0    |
| Data Type                        | Single Byte Type                | -    |   10   |   -   |  0x02   |
| Data Length                      | Following data occupies 2 Bytes | -    |   11   |   -   |  0x02   |
| Frequency Selector Knobs - Upper | 0x00~0xFF  in Two's Complement  | -    |   12   |   -   |    0    |
| Frequency Selector Knobs - Lower | 0x00~0xFF  in Two's Complement  | -    |   13   |   -   |    0    |

**About Knob Rotate Definition:**
Signed values determine rotation direction, with the magnitude representing the rotating count.
So that, this value is in Two's Complement.

## Downlink Data

The computer send to the device.

| Name                        | Note                               | Mask | Byte[] | Bit[] | Example |
|-----------------------------|------------------------------------|------|:------:|:-----:|:-------:|
| Head                        | Constant: 0xF2                     |      |   0    |   -   |  0xF2   |
| Head                        | Constant: 0xE1                     |      |   1    |   -   |  0xE1   |
| Head                        | Constant: 0x06                     |      |   2    |   -   |  0x06   |
| Data Type Total             | Has 3 Data Type                    |      |   3    |   -   |  0x02   |
| Data Type                   | Bit Type                           |      |   4    |   -   |  0x01   |
| Data Length                 | Following data occupies 3 Bytes    |      |   5    |   -   |  0x03   |
| Transfer Led                | On:1, Off: 0                       | 0x01 |   6    |   0   |    1    |
| VHF1 Signal                 | On:1, Off: 0                       | 0x02 |   6    |   1   |    1    |
| VHF2 Signal                 | On:1, Off: 0                       | 0x04 |   6    |   2   |    1    |
| VHF3 Signal                 | On:1, Off: 0                       | 0x08 |   6    |   3   |    1    |
| LOAD Signal                 | On:1, Off: 0                       | 0x10 |   6    |   4   |    1    |
| HF1 Signal                  | On:1, Off: 0                       | 0x20 |   6    |   5   |    1    |
| SEL Signal                  | On:1, Off: 0                       | 0x40 |   6    |   6   |    1    |
| HF2 Signal                  | On:1, Off: 0                       | 0x80 |   6    |   7   |    1    |
| ATC Signal                  | Circle Point, Active:1, Inactive:0 | 0x01 |   7    |   0   |    1    |
| NAV Signal                  | Active:1, Inactive:0               | 0x02 |   7    |   1   |    1    |
| VOR Signal                  | Active:1, Inactive:0               | 0x04 |   7    |   2   |    1    |
| ILS Signal                  | Active:1, Inactive:0               | 0x08 |   7    |   3   |    1    |
| GLS Signal                  | SPD:0, MACH:1                      | 0x10 |   7    |   4   |    1    |
| MLS Signal                  | HDG V/S:0, TRK FPA:1               | 0x20 |   7    |   5   |    1    |
| ADF Signal                  | Turn On All Light And LCD          | 0x40 |   7    |   6   |    1    |
| ATC MSG Upper Led           | -                                  | 0x80 |   7    |   7   |    0    |
| AUTO LAND Led               | On:1, Off:0                        | 0x01 |   8    |   0   |    1    |
| Left LCD Switch             | On:1, Off:0                        | 0x02 |   8    |   1   |    1    |
| Right LCD Switch            | On:1, Off:0                        | 0x04 |   8    |   2   |    1    |
| Left Display - "C" Mode     | On:1, Off:0, priority second.      | -    |   8    |   3   |    0    |
| Right Display - "C" Mode    | On:1, Off:0, priority second.      | -    |   8    |   4   |    0    |
| Left Display - "Data" Mode  | On:1, Off:0, priority first.       | -    |   8    |   5   |    0    |
| Right Display - "Data" Mode | On:1, Off:0  priority first.       | -    |   8    |   6   |    0    |
| ATC MSG Lower Led           | On:1, Off:0                        | -    |   8    |   7   |    0    |
| Data Type                   | Single Byte Type                   | -    |   9    |   -   |  0x02   |
| Data Length                 | Following data occupies 2 Bytes    | -    |   10   |   -   |  0x02   |
| LCD Brightness              | 0x00(Min)-0xFF(Max)                | -    |   11   |   -   |    0    |
| Background Light Brightness | 0x00(Min)-0xFF(Max)                | -    |   12   |   -   |    0    |
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

**About LCD Switch:**
Ignore other LCD operation when LCD switch off.