[English](A320%20MCDU_EN.md) | [中文](A320%20MCDU_CN.md)

# A320 MCDU 协议

USB 信息：

- VID：`0xA416`
- PID：`0xC887`
- 产品名称：`WINGFLEXA320CDU`
- 输入报告长度：65 字节
- 输出报告长度：65 字节
- HID Report ID：`0x00`

下表中的字节位置均以设备有效载荷为基准。Windows HID 缓冲区的第 0 字节是 Report ID `0x00`，设备有效载荷从第 1 字节开始。

## 上行数据

设备发送给计算机的数据。

| 名称 | 说明 | 掩码 | Byte[] | Bit[] | 示例 |
| --- | --- | --- | :---: | :---: | :---: |
| 帧头 | 固定值 | - | 0 | - | `0xF2` |
| 帧头 | 固定值 | - | 1 | - | `0xE1` |
| 设备类型 | 固定值 | - | 2 | - | `0x04` |
| 数据类型总数 | 1 种数据类型 | - | 3 | - | `0x01` |
| 数据类型 | 位类型 | - | 4 | - | `0x01` |
| 数据长度 | 按键位图占 10 字节 | - | 5 | - | `0x0A` |
| 按键位图 | 按下：1，释放：0 | 见键位表 | 6-15 | 0-7 | `0x00` |
| 保留 / 状态 | 不用于按键解析 | - | 16-63 | - | - |

### 键位表

每个字节从最低位开始排列。原始按键码计算方式：

```text
raw_key_code = (payload_byte - 6) * 8 + bit
pressed      = (payload[payload_byte] & (1 << bit)) != 0
```

| 有效载荷字节 | Bit 0 | Bit 1 | Bit 2 | Bit 3 | Bit 4 | Bit 5 | Bit 6 | Bit 7 |
| :---: | --- | --- | --- | --- | --- | --- | --- | --- |
| 6 | L1 | L2 | L3 | L4 | L5 | L6 | R1 | R2 |
| 7 | R3 | R4 | R5 | R6 | DIR | PROG | PERF | INIT |
| 8 | DATA | BLANK1 | F-PLN | RAD/NAV | FUEL/PRED | SEC F-PLAN | ATC COMM | MCDU MENU |
| 9 | BRT | DIM | AIRPORT | BLANK2 | 左箭头 | 上箭头 | 右箭头 | 下箭头 |
| 10 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| 11 | 9 | 小数点 | 0 | +/- | A | B | C | D |
| 12 | E | F | G | H | I | J | K | L |
| 13 | M | N | O | P | Q | R | S | T |
| 14 | U | V | W | X | Y | Z | 斜杠 | SP |
| 15 | OVFY | CLR | 选择 / 偏移状态 | 保留 | 保留 | 保留 | 保留 | 保留 |

`BLANK1` 是 DATA 右侧的空白键，`BLANK2` 是 AIRPORT 右侧的空白键。

原始码 `0..73` 对应实体按键。原始码 `74` 是选择/偏移状态；该状态有效时，逻辑按键码计算方式如下：

```text
logical_key_code = raw_key_code + 75
```

输入报告频率约为 10 Hz。

## 下行数据

计算机向设备发送屏幕和灯光数据。先生成 567 字节核心数据，再拆分成 9 个 63 字节数据块，并发送全部 9 个输出报告。

### 核心数据

| 名称 | 说明 | 核心 Byte[] | 长度 | 取值 |
| --- | --- | :---: | :---: | --- |
| 设备类型 | 固定值 | 0 | 1 | `0x04` |
| 屏幕亮度 | 最低到最高 | 1 | 1 | `0x00..0x17` |
| 按键背光亮度 | 最低到最高 | 2 | 1 | `0x00..0x17` |
| MCDU MENU 灯 | 灭 / 亮 | 3 | 1 | `0x00` / `0x01` |
| FAIL 灯 | 灭 / 亮 | 4 | 1 | `0x00` / `0x01` |
| FM 灯 | 灭 / 亮 | 5 | 1 | `0x00` / `0x01` |
| FM1 灯 | 灭 / 亮 | 6 | 1 | `0x00` / `0x01` |
| IND 灯 | 灭 / 亮 | 7 | 1 | `0x00` / `0x01` |
| RDY 灯 | 灭 / 亮 | 8 | 1 | `0x00` / `0x01` |
| LINE 灯 | 灭 / 亮 | 9 | 1 | `0x00` / `0x01` |
| FM2 灯 | 灭 / 亮 | 10 | 1 | `0x00` / `0x01` |
| 屏幕单元格 | 24 列 × 14 行 | 11-514 | 504 | 见下文 |
| 填充 | 使用零填充 | 515-566 | 52 | `0x00` |

两个亮度字段均不得使用大于 `0x17` 的值。

### 屏幕单元格

屏幕为 24 列（`x = 0..23`）、14 行（`y = 0..13`）。按列优先顺序序列化：外层循环为 `x`，内层循环为 `y`。

每个单元格包含：

- 1 字节字符；标准字符使用 ASCII 值；
- 1 个 `0x0..0xF` 范围内的 4 位属性值。

每两个连续单元格编码为 3 字节：

```text
character[x, y]
character[x, y + 1]
(attribute[x, y] << 4) | attribute[x, y + 1]
```

屏幕数据由 336 个字符字节和 168 个压缩属性字节交错组成，共 504 字节。

### 输出报告

将 567 字节核心数据拆分为 9 个 63 字节数据块。分片编号 `n = 1..9`：

```text
device_fragment = n + core[(n - 1) * 63 .. n * 63 - 1]
windows_report  = 0x00 + device_fragment
```

每个 Windows 输出报告固定为 65 字节：

| Byte[] | 长度 | 取值 |
| :---: | :---: | --- |
| 0 | 1 | HID Report ID `0x00` |
| 1 | 1 | 分片编号 `0x01..0x09` |
| 2-64 | 63 | 对应的核心数据块 |

按编号升序发送分片。屏幕或灯光状态变化时发送完整的 9 分片帧。同一时间只能由一个应用程序向设备写入输出报告。

### 序列化示例

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
