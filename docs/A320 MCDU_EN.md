[English](A320%20MCDU_EN.md) | [中文](A320%20MCDU_CN.md)

# A320 MCDU Protocol

USB Information:

- VID: `0xA416`
- PID: `0xC887`
- Product: `WINGFLEXA320CDU`
- Input report length: 65 bytes
- Output report length: 65 bytes
- HID Report ID: `0x00`

Byte positions in the tables below refer to the device payload. A Windows HID buffer adds Report ID `0x00` at byte 0, so its payload begins at byte 1.

## Uplink Data

The device sends data to the computer.

| Name | Note | Mask | Byte[] | Bit[] | Example |
| --- | --- | --- | :---: | :---: | :---: |
| Head | Constant | - | 0 | - | `0xF2` |
| Head | Constant | - | 1 | - | `0xE1` |
| Device Type | Constant | - | 2 | - | `0x04` |
| Data Type Total | One data type | - | 3 | - | `0x01` |
| Data Type | Bit type | - | 4 | - | `0x01` |
| Data Length | Key bitmap occupies 10 bytes | - | 5 | - | `0x0A` |
| Key Bitmap | Press: 1, Release: 0 | See key map | 6-15 | 0-7 | `0x00` |
| Reserved / Status | Do not use for key decoding | - | 16-63 | - | - |

### Key Map

Bits are ordered least-significant bit first. The raw key code is:

```text
raw_key_code = (payload_byte - 6) * 8 + bit
pressed      = (payload[payload_byte] & (1 << bit)) != 0
```

| Payload Byte | Bit 0 | Bit 1 | Bit 2 | Bit 3 | Bit 4 | Bit 5 | Bit 6 | Bit 7 |
| :---: | --- | --- | --- | --- | --- | --- | --- | --- |
| 6 | L1 | L2 | L3 | L4 | L5 | L6 | R1 | R2 |
| 7 | R3 | R4 | R5 | R6 | DIR | PROG | PERF | INIT |
| 8 | DATA | BLANK1 | F-PLN | RAD/NAV | FUEL/PRED | SEC F-PLAN | ATC COMM | MCDU MENU |
| 9 | BRT | DIM | AIRPORT | BLANK2 | LEFT ARROW | UP ARROW | RIGHT ARROW | DOWN ARROW |
| 10 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| 11 | 9 | DOT | 0 | +/- | A | B | C | D |
| 12 | E | F | G | H | I | J | K | L |
| 13 | M | N | O | P | Q | R | S | T |
| 14 | U | V | W | X | Y | Z | SLASH | SP |
| 15 | OVFY | CLR | Selector / Shift | Reserved | Reserved | Reserved | Reserved | Reserved |

`BLANK1` is the blank key to the right of DATA. `BLANK2` is the blank key to the right of AIRPORT.

Raw codes `0..73` identify the physical keys. Raw code `74` is the selector/shift state. When it is active, logical key codes are calculated as follows:

```text
logical_key_code = raw_key_code + 75
```

The input report rate is approximately 10 Hz.

## Downlink Data

The computer sends display and lighting data to the device. Build a 567-byte core, split it into nine 63-byte blocks, and send all nine output reports.

### Core Payload

| Name | Note | Core Byte[] | Length | Value |
| --- | --- | :---: | :---: | --- |
| Device Type | Constant | 0 | 1 | `0x04` |
| Screen Brightness | Minimum to maximum | 1 | 1 | `0x00..0x17` |
| Key Backlight Brightness | Minimum to maximum | 2 | 1 | `0x00..0x17` |
| MCDU MENU Light | Off / On | 3 | 1 | `0x00` / `0x01` |
| FAIL Light | Off / On | 4 | 1 | `0x00` / `0x01` |
| FM Light | Off / On | 5 | 1 | `0x00` / `0x01` |
| FM1 Light | Off / On | 6 | 1 | `0x00` / `0x01` |
| IND Light | Off / On | 7 | 1 | `0x00` / `0x01` |
| RDY Light | Off / On | 8 | 1 | `0x00` / `0x01` |
| LINE Light | Off / On | 9 | 1 | `0x00` / `0x01` |
| FM2 Light | Off / On | 10 | 1 | `0x00` / `0x01` |
| Display Cells | 24 columns × 14 rows | 11-514 | 504 | See below |
| Padding | Fill with zero | 515-566 | 52 | `0x00` |

Do not use values above `0x17` for either brightness field.

### Display Cells

The screen contains 24 columns (`x = 0..23`) and 14 rows (`y = 0..13`). Cells are serialized in column-major order: `x` is the outer loop and `y` is the inner loop.

Each cell has:

- one character byte; ASCII values are used for standard characters;
- one 4-bit attribute value in the range `0x0..0xF`.

Two consecutive cells are encoded into three bytes:

```text
character[x, y]
character[x, y + 1]
(attribute[x, y] << 4) | attribute[x, y + 1]
```

This produces 336 character bytes and 168 packed attribute bytes, interleaved into 504 bytes.

### Output Reports

Split the 567-byte core into nine 63-byte blocks. For fragment number `n = 1..9`:

```text
device_fragment = n + core[(n - 1) * 63 .. n * 63 - 1]
windows_report  = 0x00 + device_fragment
```

Every Windows output report is exactly 65 bytes:

| Byte[] | Length | Value |
| :---: | :---: | --- |
| 0 | 1 | HID Report ID `0x00` |
| 1 | 1 | Fragment number `0x01..0x09` |
| 2-64 | 63 | Corresponding core block |

Send fragments in ascending order. Send a complete nine-fragment frame whenever the screen or lighting state changes. Only one application should write output reports to the device at a time.

### Serializer Example

```text
core = [0x04, screenBrightness, backlightBrightness,
        menu, fail, fm, fm1, ind, rdy, line, fm2]

for x = 0..23:
    for y = 0, 2, 4, 6, 8, 10, 12:
        core.append(character[x, y])
        core.append(character[x, y + 1])
        core.append((attribute[x, y] << 4) | attribute[x, y + 1])

while core.length < 567:
    core.append(0x00)

for fragment = 1..9:
    block = core[(fragment - 1) * 63 .. fragment * 63 - 1]
    hid_write([0x00, fragment] + block)
```
