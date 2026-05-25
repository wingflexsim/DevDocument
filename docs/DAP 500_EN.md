# DAP 500 Communication Protocol

## Product Features

This is the first product to fully support a universal control protocol. Key features:
1. Supports direct in-game key/axis data binding.
2. Supports rapid integration and development in virtually all programming languages.
3. INPUT reports are only sent when data changes.
4. OUTPUT reports only need to be sent once within a 10-second window to maintain device state.

## Design Specifications

1. Buttons and encoders use the HID Generic INPUT protocol, mapped to JoyStick Axis and Button, which users can bind freely and are recognized in-game.
2. Button lighting uses the HID Custom OUTPUT protocol, controlled by the host software.

## PID & VID

Normal Operation Mode:
- VID: 0xC687
- PID: 0xB216

## INPUT Report

**REPORT_ID = 1**

Data flow: Device to Computer.

### Total Report Length

5 bytes

### Report Description

Button pressed value = 1, button released value = 0.

| Byte Index | Function Name | Data Type | Bit Field | Description                                            |
|------------|---------------|-----------|-----------|--------------------------------------------------------|
| 0          | REPORT_ID     | uint8_t   | -         | ReportID                                               |
| 1          | HDG_EC_L      | uint8_t   | Bit 0     | Heading encoder rotate left                            |
| 1          | HDG_EC_R      | uint8_t   | Bit 1     | Heading encoder rotate right                           |
| 1          | HDG_EC_SW     | uint8_t   | Bit 2     | Heading encoder button press                           |
| 1          | NOSE_DOWN     | uint8_t   | Bit 3     | Vertical encoder pitch up                              |
| 1          | NOSE_UP       | uint8_t   | Bit 4     | Vertical encoder pitch down                            |
| 1          | ALT_EC_L      | uint8_t   | Bit 5     | Altitude encoder rotate left                           |
| 1          | ALT_EC_R      | uint8_t   | Bit 6     | Altitude encoder rotate right                          |
| 1          | ALT_EC_SW     | uint8_t   | Bit 7     | Altitude encoder button press                          |
| 2          | HDG           | uint8_t   | Bit 0     | Heading hold button                                    |
| 2          | APR           | uint8_t   | Bit 1     | Approach button                                        |
| 2          | NAV           | uint8_t   | Bit 2     | Navigation button                                      |
| 2          | TRK           | uint8_t   | Bit 3     | Track button                                           |
| 2          | AP            | uint8_t   | Bit 4     | Autopilot button                                       |
| 2          | FD            | uint8_t   | Bit 5     | Flight director button                                 |
| 2          | LVL           | uint8_t   | Bit 6     | Level change button, can bind to FCTL if not available |
| 2          | YD            | uint8_t   | Bit 7     | Yaw damper button                                      |
| 3          | IAS           | uint8_t   | Bit 0     | Indicated airspeed button                              |
| 3          | VNAV          | uint8_t   | Bit 1     | Vertical navigation button                             |
| 3          | VS            | uint8_t   | Bit 2     | Vertical speed hold button                             |
| 3          | ALT           | uint8_t   | Bit 3     | Altitude hold button                                   |
| 3          | Reserved      | uint8_t   | Bit 4-7   | (Reserved)                                             |
| 4          | Light Sensor  | uint8_t   | -         | Ambient light sensor, value range 0-128                |

### Structure Diagram

```
Byte 0: [REPORT_ID]
Byte 1: [ALT_EC_SW][ALT_EC_R][ALT_EC_L][NOSE_UP][NOSE_DOWN][HDG_EC_SW][HDG_EC_R][HDG_EC_L]
Byte 2: [YD][LVL][FD][AP][TRK][NAV][APR][HDG]
Byte 3: [Reserved][Reserved][Reserved][Reserved][ALT][VS][VNAV][IAS]
```

## OUTPUT Report

**REPORT_ID = 2**

Data flow: Computer to Device.

### Total Report Length

5 bytes

### Report Description

Arrow indicator LEDs: ON value = 1, OFF value = 0.

| Byte Index | Function Name        | Data Type | Bit Field | Description                                                                   |
|------------|----------------------|-----------|-----------|-------------------------------------------------------------------------------|
| 0          | REPORT_ID            | uint8_t   | -         | ReportID                                                                      |
| 1          | Method               | uint8_t   | -         | Request method. Currently defined: 1=DAP lighting, 2=Expansion panel lighting |
| 2          | APR LED              | uint8_t   | Bit 0     | APR arrow indicator LED                                                       |
| 2          | NAV LED              | uint8_t   | Bit 1     | NAV arrow indicator LED                                                       |
| 2          | TRK LED              | uint8_t   | Bit 2     | TRK arrow indicator LED                                                       |
| 2          | HDG LED              | uint8_t   | Bit 3     | HDG arrow indicator LED                                                       |
| 2          | AP LED               | uint8_t   | Bit 4     | AP arrow indicator LED                                                        |
| 2          | FD LED               | uint8_t   | Bit 5     | FD arrow indicator LED                                                        |
| 2          | LVL LED              | uint8_t   | Bit 6     | LVL arrow indicator LED                                                       |
| 2          | YD LED               | uint8_t   | Bit 7     | YD arrow indicator LED                                                        |
| 3          | IAS LED              | uint8_t   | Bit 0     | IAS arrow indicator LED                                                       |
| 3          | VNAV LED             | uint8_t   | Bit 1     | VNAV arrow indicator LED                                                      |
| 3          | VS LED               | uint8_t   | Bit 2     | VS arrow indicator LED                                                        |
| 3          | ALT LED              | uint8_t   | Bit 3     | ALT arrow indicator LED                                                       |
| 3          | Reserved             | uint8_t   | Bit 4-7   | (Reserved)                                                                    |
| 4          | Backlight Brightness | uint8_t   | -         | Backlight brightness (value: 0-255)                                           |

### Structure Diagram

```
Byte 0:  [REPORT_ID]
Byte 1:  [Method]
Byte 2:  [YD][LVL][FD][AP][HDG][TRK][NAV][APR]
Byte 3:  [Reserved][Reserved][Reserved][Reserved][ALT][VS][VNAV][IAS]
Byte 4:  [Backlight Brightness]
```

---

> **Note**: This document was translated by AI. For any discrepancies, please refer to the Chinese version [`DAP 500_CN.md`](DAP%20500_CN.md).
