# DAP 500 Communication Protocol

Updated: 2026-06-03

## Product Features

DAP 500 is a product that fully supports a universal control protocol. Key features:
1. Supports direct in-game key/axis data binding.
2. Supports rapid integration and development in virtually all programming languages.
3. INPUT reports are only sent when data changes.
4. FEATURE reports, once sent, maintain the device lighting state; auto-standby time can be configured.

## Design Specifications

1. Buttons and axes use the HID Generic INPUT protocol, mapped to JoyStick Axis and Button, which users can bind freely and are recognized in-game.
2. Button lighting uses the HID Custom FEATURE protocol, controlled by the host software.

## PID & VID

- VID: 0xC687
- PID: 0xB216

## INPUT Report id=1

**REPORT_ID = 1**

### Total Report Length

5 bytes

### Report Description

- Reports button states.
- Reports ambient light sensor status.

| Byte Index | Function Name | Data Type | Bit Field | Description                                                    |
|:-----------|---------------|-----------|:----------|:---------------------------------------------------------------|
| 0          | REPORT_ID     | uint8_t   | -         | ReportID                                                       |
| 1          | HDG_EC_L      | uint8_t   | Bit 0     | Heading encoder rotate left, pressed=1, released=0             |
| 1          | HDG_EC_R      | uint8_t   | Bit 1     | Heading encoder rotate right, pressed=1, released=0            |
| 1          | HDG_EC_SW     | uint8_t   | Bit 2     | Heading encoder button press, pressed=1, released=0            |
| 1          | NOSE_DOWN     | uint8_t   | Bit 3     | Vertical encoder pitch up, pressed=1, released=0               |
| 1          | NOSE_UP       | uint8_t   | Bit 4     | Vertical encoder pitch down, pressed=1, released=0             |
| 1          | ALT_EC_L      | uint8_t   | Bit 5     | Altitude encoder rotate left, pressed=1, released=0            |
| 1          | ALT_EC_R      | uint8_t   | Bit 6     | Altitude encoder rotate right, pressed=1, released=0           |
| 1          | ALT_EC_SW     | uint8_t   | Bit 7     | Altitude encoder button press, pressed=1, released=0           |
| 2          | HDG           | uint8_t   | Bit 0     | Heading hold button, pressed=1, released=0                     |
| 2          | APR           | uint8_t   | Bit 1     | Approach button, pressed=1, released=0                         |
| 2          | NAV           | uint8_t   | Bit 2     | Navigation button, pressed=1, released=0                       |
| 2          | TRK           | uint8_t   | Bit 3     | Track button, pressed=1, released=0                            |
| 2          | AP            | uint8_t   | Bit 4     | Autopilot button, pressed=1, released=0                        |
| 2          | FD            | uint8_t   | Bit 5     | Flight director button, pressed=1, released=0                  |
| 2          | LVL           | uint8_t   | Bit 6     | Level change button, pressed=1, released=0                     |
| 2          | YD            | uint8_t   | Bit 7     | Yaw damper button, pressed=1, released=0                       |
| 3          | IAS           | uint8_t   | Bit 0     | Indicated airspeed button, pressed=1, released=0               |
| 3          | VNAV          | uint8_t   | Bit 1     | Vertical navigation button, pressed=1, released=0              |
| 3          | VS            | uint8_t   | Bit 2     | Vertical speed hold button, pressed=1, released=0              |
| 3          | ALT           | uint8_t   | Bit 3     | Altitude hold button, pressed=1, released=0                    |
| 3          | Reserved      | uint8_t   | Bit 4-7   | (Reserved)                                                     |
| 4          | Light Sensor  | uint8_t   | -         | Ambient light sensor, value range 0-128                        |

### Structure Diagram

```
Byte 0: [REPORT_ID]
Byte 1: [ALT_EC_SW][ALT_EC_R][ALT_EC_L][NOSE_UP][NOSE_DOWN][HDG_EC_SW][HDG_EC_R][HDG_EC_L]
Byte 2: [YD][LVL][FD][AP][TRK][NAV][APR][HDG]
Byte 3: [Reserved][Reserved][Reserved][Reserved][ALT][VS][VNAV][IAS]
Byte 4: [Light Sensor]
```

## Feature SET_REPORT id=2

**REPORT_ID = 2**

### Total Report Length

5 bytes

### Report Description

- Sets button arrow indicator LEDs.
- Sets backlight brightness.

| Byte Index | Function Name        | Data Type | Bit Field | Description                                              |
|:-----------|----------------------|-----------|:----------|:---------------------------------------------------------|
| 0          | REPORT_ID            | uint8_t   | -         | ReportID                                                 |
| 1          | APR LED              | uint8_t   | Bit 0     | APR arrow indicator LED, on=1, off=0 (default)           |
| 1          | NAV LED              | uint8_t   | Bit 1     | NAV arrow indicator LED, on=1, off=0 (default)           |
| 1          | TRK LED              | uint8_t   | Bit 2     | TRK arrow indicator LED, on=1, off=0 (default)           |
| 1          | HDG LED              | uint8_t   | Bit 3     | HDG arrow indicator LED, on=1, off=0 (default)           |
| 1          | AP LED               | uint8_t   | Bit 4     | AP arrow indicator LED, on=1, off=0 (default)            |
| 1          | FD LED               | uint8_t   | Bit 5     | FD arrow indicator LED, on=1, off=0 (default)            |
| 1          | LVL LED              | uint8_t   | Bit 6     | LVL arrow indicator LED, on=1, off=0 (default)           |
| 1          | YD LED               | uint8_t   | Bit 7     | YD arrow indicator LED, on=1, off=0 (default)            |
| 2          | IAS LED              | uint8_t   | Bit 0     | IAS arrow indicator LED, on=1, off=0 (default)           |
| 2          | VNAV LED             | uint8_t   | Bit 1     | VNAV arrow indicator LED, on=1, off=0 (default)          |
| 2          | VS LED               | uint8_t   | Bit 2     | VS arrow indicator LED, on=1, off=0 (default)            |
| 2          | ALT LED              | uint8_t   | Bit 3     | ALT arrow indicator LED, on=1, off=0 (default)           |
| 2          | Reserved             | uint8_t   | Bit 4-7   | (Reserved)                                               |
| 3          | Backlight Brightness | uint8_t   | -         | Backlight brightness (value: 0-255), default value: 255  |
| 4          | Reserved             | uint8_t   | -         | (Reserved)                                               |

### Structure Diagram

```
Byte 0:  [REPORT_ID]
Byte 1:  [YD][LVL][FD][AP][HDG][TRK][NAV][APR]
Byte 2:  [Reserved][Reserved][Reserved][Reserved][ALT][VS][VNAV][IAS]
Byte 3:  [Auto Backlight]
Byte 4:  [Backlight Brightness]
```

## Feature GET_REPORT id=2

**REPORT_ID = 2**

### Total Report Length

5 bytes

### Report Description

- Reports button states.
- Reports ambient light sensor status.

| Byte Index | Function Name | Data Type | Bit Field | Description                                                    |
|:-----------|---------------|-----------|:----------|:---------------------------------------------------------------|
| 0          | REPORT_ID     | uint8_t   | -         | ReportID                                                       |
| 1          | HDG_EC_L      | uint8_t   | Bit 0     | Heading encoder rotate left, pressed=1, released=0             |
| 1          | HDG_EC_R      | uint8_t   | Bit 1     | Heading encoder rotate right, pressed=1, released=0            |
| 1          | HDG_EC_SW     | uint8_t   | Bit 2     | Heading encoder button press, pressed=1, released=0            |
| 1          | NOSE_DOWN     | uint8_t   | Bit 3     | Vertical encoder pitch up, pressed=1, released=0               |
| 1          | NOSE_UP       | uint8_t   | Bit 4     | Vertical encoder pitch down, pressed=1, released=0             |
| 1          | ALT_EC_L      | uint8_t   | Bit 5     | Altitude encoder rotate left, pressed=1, released=0            |
| 1          | ALT_EC_R      | uint8_t   | Bit 6     | Altitude encoder rotate right, pressed=1, released=0           |
| 1          | ALT_EC_SW     | uint8_t   | Bit 7     | Altitude encoder button press, pressed=1, released=0           |
| 2          | HDG           | uint8_t   | Bit 0     | Heading hold button, pressed=1, released=0                     |
| 2          | APR           | uint8_t   | Bit 1     | Approach button, pressed=1, released=0                         |
| 2          | NAV           | uint8_t   | Bit 2     | Navigation button, pressed=1, released=0                       |
| 2          | TRK           | uint8_t   | Bit 3     | Track button, pressed=1, released=0                            |
| 2          | AP            | uint8_t   | Bit 4     | Autopilot button, pressed=1, released=0                        |
| 2          | FD            | uint8_t   | Bit 5     | Flight director button, pressed=1, released=0                  |
| 2          | LVL           | uint8_t   | Bit 6     | Level change button, pressed=1, released=0                     |
| 2          | YD            | uint8_t   | Bit 7     | Yaw damper button, pressed=1, released=0                       |
| 3          | IAS           | uint8_t   | Bit 0     | Indicated airspeed button, pressed=1, released=0               |
| 3          | VNAV          | uint8_t   | Bit 1     | Vertical navigation button, pressed=1, released=0              |
| 3          | VS            | uint8_t   | Bit 2     | Vertical speed hold button, pressed=1, released=0              |
| 3          | ALT           | uint8_t   | Bit 3     | Altitude hold button, pressed=1, released=0                    |
| 3          | Reserved      | uint8_t   | Bit 4-7   | (Reserved)                                                     |
| 4          | Light Sensor  | uint8_t   | -         | Ambient light sensor, value range 0-128                        |

### Structure Diagram

```
Byte 0:  [REPORT_ID]
Byte 1:  [ALT_EC_SW][ALT_EC_R][ALT_EC_L][NOSE_UP][NOSE_DOWN][HDG_EC_SW][HDG_EC_R][HDG_EC_L]
Byte 2:  [YD][LVL][FD][AP][TRK][NAV][APR][HDG]
Byte 3:  [Reserved][Reserved][Reserved][Reserved][ALT][VS][VNAV][IAS]
Byte 4:  [Light Sensor]
```

## Feature GET_REPORT id=3

**REPORT_ID = 3**

### Total Report Length

5 bytes

### Report Description

- Reports hardware and firmware version numbers.

| Byte Index | Function Name     | Data Type | Bit Field | Description            |
|:-----------|-------------------|-----------|:----------|:-----------------------|
| 0          | REPORT_ID         | uint8_t   | -         | ReportID               |
| 1          | HW Version         | uint8_t   | -         | Hardware Version       |
| 2          | FW Version Major   | uint8_t   | -         | Firmware Version Major |
| 3          | FW Version Minor   | uint8_t   | -         | Firmware Version Minor |
| 4          | FW Version Patch   | uint8_t   | -         | Firmware Version Patch |

### Structure Diagram

```
Byte 0: [REPORT_ID]
Byte 1: [HW Version]
Byte 2: [FW Version Major]
Byte 3: [FW Version Minor]
Byte 4: [FW Version Patch]
```

## Feature SET_REPORT id=4

**REPORT_ID = 4**

### Total Report Length

5 bytes

### Report Description

- Reports custom settings.

| Byte Index | Function Name               | Data Type | Bit Field | Description                                                                                          |
|:-----------|-----------------------------|-----------|:----------|:-----------------------------------------------------------------------------------------------------|
| 0          | REPORT_ID                   | uint8_t   | -         | ReportID                                                                                             |
| 1          | Auto Backlight Enable       | uint8_t   | Bit 0     | Enable auto backlight, on=1, off=0 (default)                                                          |
| 1          | Light Sensor Report Enable  | uint8_t   | Bit 1     | Enable light sensor reporting, on=1 (default), off=0                                                  |
| 1          | Reserved                    | uint8_t   | Bit 2-7   | (Reserved)                                                                                           |
| 2          | Reserved                    | uint8_t   | -         | (Reserved)                                                                                           |
| 3-4        | Auto Standby Time           | uint16_t  | -         | Auto standby time (unit: seconds). Lights are automatically turned off after the specified time of inactivity. Default value = 5 (sec), maximum 65535 |

## Feature GET_REPORT id=4

**REPORT_ID = 4**

### Total Report Length

5 bytes

### Report Description

- Reports custom settings.

| Byte Index | Function Name              | Data Type | Bit Field | Description                                                                                                                                           |
|:-----------|----------------------------|-----------|:----------|:------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0          | REPORT_ID                  | uint8_t   | -         | ReportID                                                                                                                                              |
| 1          | Auto Backlight Enable      | uint8_t   | Bit 0     | Enable auto backlight, on=1, off=0 (default)                                                                                                          |
| 1          | Light Sensor Report Enable | uint8_t   | Bit 1     | Enable light sensor reporting, on=1 (default), off=0                                                                                                  |
| 1          | Reserved                   | uint8_t   | Bit 2-7   | (Reserved)                                                                                                                                            |
| 2          | Reserved                   | uint8_t   | -         | (Reserved)                                                                                                                                            |
| 3-4        | Auto Standby Time          | uint16_t  | -         | Auto standby time (unit: seconds). Lights are automatically turned off after the specified time of inactivity. Default value = 5 (sec), maximum 65535 |

---

> **Note**: This document was translated by AI. For any discrepancies, please refer to the Chinese version [`DAP 500_CN.md`](DAP%20500_CN.md).
