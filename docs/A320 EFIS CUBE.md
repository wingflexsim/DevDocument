# A320 EFIS CUBE Protocol

USB Information:

- VID: 0xA516
- PID: 0xC987

## Uplink Data

The device send to the computer.

| Name            | Note                            | Mask | Byte[] | Bit[] | Example |
|-----------------|---------------------------------|------|:------:|:-----:|:-------:|
| Head            | Constant: 0xF2                  |      |   0    |   -   |  0xF2   |
| Head            | Constant: 0xE1                  |      |   1    |   -   |  0xE1   |
| Head            | Constant: 0x05                  |      |   2    |   -   |  0x05   |
| Data Type Total | Has 2 Data Type                 |      |   3    |   -   |  0x02   |
| Data Type       | Bit Type                        |      |   4    |   -   |  0x01   |
| Data Length     | Following data occupies 4 Bytes |      |   5    |   -   |  0x04   |
| MASTER WRAM     | Press:1, Release: 0             | 0x01 |   6    |   0   |    1    |
| MASTER CAUT     | Press:1, Release: 0             | 0x02 |   6    |   1   |    1    |
| CHRONO          | Press:1, Release: 0             | 0x04 |   6    |   2   |    1    |
| STICK PRIORITY  | Press: 1, Release: 0            | 0x08 |   6    |   3   |    1    |
| FD              | Press: 1, Release: 0            | 0x10 |   6    |   4   |    1    |
| LS              | Press: 1, Release: 0            | 0x20 |   6    |   5   |    1    |
| CSTR            | Press: 1, Release: 0            | 0x40 |   6    |   6   |    1    |
| WPT             | Press: 1, Release: 0            | 0x80 |   6    |   7   |    1    |
| VOR.D           | Push: 1, Release: 0             | 0x01 |   7    |   0   |    1    |
| NDB             | Pull: 1, Release: 0             | 0x02 |   7    |   1   |    1    |
| ARPT            | Push: 1, Release: 0             | 0x04 |   7    |   2   |    1    |
| inHg            | Pull: 1, Release: 0             | 0x08 |   7    |   3   |    1    |
| hPa             | Press: 1, Release: 0            | 0x10 |   7    |   4   |    1    |
| Rotary LS       | Pointing: 1, Non-pointing: 0    | 0x20 |   7    |   5   |    1    |
| Rotary VOR      | Pointing: 1, Non-pointing: 0    | 0x40 |   7    |   6   |    1    |
| Rotary NAV      | Pointing: 1, Non-pointing: 0    | 0x80 |   7    |   7   |    1    |
| Rotary ARC      | Pointing: 1, Non-pointing: 0    | 0x01 |   8    |   0   |    1    |
| Rotary PLAN     | Pointing: 1, Non-pointing: 0    | 0x02 |   8    |   1   |    1    |
| Rotary 10       | Pointing: 1, Non-pointing: 0    | 0x04 |   8    |   2   |    1    |
| Rotary 20       | Pointing: 1, Non-pointing: 0    | 0x08 |   8    |   3   |    0    |
| Rotary 40       | Pointing: 1, Non-pointing: 0    | 0x10 |   8    |   4   |    0    |
| Rotary 80       | Pointing: 1, Non-pointing: 0    | 0x20 |   8    |   5   |    0    |
| Rotary 160      | Pointing: 1, Non-pointing: 0    | 0x40 |   8    |   6   |    0    |
| Rotary 320      | Pointing: 1, Non-pointing: 0    | 0x80 |   8    |   7   |    0    |
| ADF1            | Enale:1, Diable: 0              | 0x01 |   9    |   0   |    0    |
| OFF1            | Enale:1, Diable: 0              | 0x02 |   9    |   1   |    1    |
| VOR1            | Enale:1, Diable: 0              | 0x04 |   9    |   2   |    0    |
| ADF2            | Enale:1, Diable: 0              | 0x08 |   9    |   3   |    0    |
| OFF2            | Enale:1, Diable: 0              | 0x10 |   9    |   4   |    1    |
| VOR2            | Enale:1, Diable: 0              | 0x20 |   9    |   5   |    0    |
| Baro Push       | Enale:1, Diable: 0              | 0x40 |   9    |   6   |    0    |
| Baro Pull       | Enale:1, Diable: 0              | 0x80 |   9    |   7   |    0    |
| Data Type       | Single Byte Type                | -    |   10   |   -   |  0x02   |
| Data Length     | Following data occupies 1 Bytes | -    |   11   |   -   |  0x01   |
| Baro Encoder    | 0x00 ~ 0xFF                     | -    |   12   |   -   |    0    |

**About Knob Rotate Definition:**
Signed values determine rotation direction, with the magnitude representing the rotating count.
So that, this value is in Two's Complement.

## Downlink Data

The computer send to the device.

| Name                        | Note                            | Mask | Byte[] | Bit[] | Example |
|-----------------------------|---------------------------------|------|:------:|:-----:|:-------:|
| Head                        | Constant: 0xF2                  |      |   0    |   -   |  0xF2   |
| Head                        | Constant: 0xE1                  |      |   1    |   -   |  0xE1   |
| Head                        | Constant: 0x05                  |      |   2    |   -   |  0x05   |
| Data Type Total             | Has 3 Data Type                 |      |   3    |   -   |  0x03   |
| Data Type                   | Bit Type                        |      |   4    |   -   |  0x01   |
| Data Length                 | Following data occupies 3 Bytes |      |   5    |   -   |  0x03   |
| MASTER WRAN LIGHT           | On:1, Off: 0                    | 0x01 |   6    |   0   |    1    |
| MASTER CAUT LIGHT           | On:1, Off: 0                    | 0x02 |   6    |   1   |    1    |
| CAPT Arrow                  | On:1, Off: 0                    | 0x04 |   6    |   2   |    1    |
| CAPT                        | On:1, Off: 0                    | 0x08 |   6    |   3   |    1    |
| FD LIGHT                    | On:1, Off: 0                    | 0x10 |   6    |   4   |    1    |
| LS LIGHT                    | On:1, Off: 0                    | 0x20 |   6    |   5   |    1    |
| CSTR LIGHT                  | On:1, Off: 0                    | 0x40 |   6    |   6   |    1    |
| WPT LIGHT                   | On:1, Off: 0                    | 0x80 |   6    |   7   |    1    |
| VOR.D LIGHT                 | On:1, Off: 0                    | 0x01 |   7    |   0   |    1    |
| NDB LIGHT                   | On:1, Off: 0                    | 0x02 |   7    |   1   |    1    |
| ARPT LIGHT                  | On:1, Off: 0                    | 0x04 |   7    |   2   |    1    |
| Light Control Mode          | By Host:1(Default), By Slave:0  | 0x08 |   7    |   3   |    1    |
| LCD QFE Tag                 | On:1, Off: 0                    | 0x10 |   7    |   4   |    1    |
| LCD QNH Tag                 | On:1, Off: 0                    | 0x20 |   7    |   5   |    1    |
| LCD Dot(.)                  | On:1, Off: 0                    | 0x40 |   7    |   6   |    1    |
| LCD STD Mode                | On:1, Off: 0                    | 0x80 |   7    |   7   |    0    |
| Power                       | On:1, Off:0                     | 0x01 |   8    |   0   |    1    |
| (Reserve)                   |                                 | -    |   8    |   1   |    0    |
| (Reserve)                   |                                 | -    |   8    |   2   |    0    |
| (Reserve)                   |                                 | -    |   8    |   3   |    0    |
| (Reserve)                   |                                 | -    |   8    |   4   |    0    |
| (Reserve)                   |                                 | -    |   8    |   5   |    0    |
| (Reserve)                   |                                 | -    |   8    |   6   |    0    |
| (Reserve)                   |                                 | -    |   8    |   7   |    0    |
| Data Type                   | Single Byte Type                | -    |   9    |   -   |  0x02   |
| Data Length                 | Following data occupies 2 Bytes | -    |   10   |   -   |  0x02   |
| Background Light Brightness | 0x00(Minimum)-0xFF(Maximum)     | -    |   11   |   -   |    0    |
| LCD Brightness              | 0x00(Minimum)-0xFF(Maximum)     | -    |   12   |   -   |    0    |
| Data Type                   | Double Byte Type                | -    |   13   |   -   |  0x03   |
| Data Length                 | Following data occupies 2 Bytes | -    |   14   |   -   |  0x02   |
| inHg-hPa Number             | High 8 bit of Uint16            | -    |   15   |   -   |  0x00   |
| inHg-hPa Number             | Low 8 bit of Uint16             | -    |   16   |   -   |  0x00   |

**About Power:**
To make any light turn on, You must set Power=1.