# DAP 500 通讯协议

## 产品特点

这是首款完全支持通用控制协议的产品。具有以下特点：
1. 支持游戏内直接绑定按键或轴数据输入。
2. 支持几乎所有语言快捷接入开发。
3. INPUT 报告仅在数据更新时上报。
4. OUTPUT 报告只需10s秒内有一次下发便会保持设备状态。

## 设计规范

1. 按键和轴使用 HID 通用 INPUT 协议，映射为JoyStick 的 Axis 和 Button，用户可自行绑定，游戏内可以识别。
2. 按键灯光使用 HID 自定义 OUTPUT 协议，由上位机控制。

## PID & VID

正常工作模式：
- VID: 0xC687
- PID: 0xB216

## INPUT 输入报告

**REPORT_ID = 1**

由设备输入到电脑。

### 报告总长度

5 字节

### 报告描述

按键按下值=1，按键松开值=0。

| 字节索引 | 功能名称         | 数据类型    | 位域      | 功能描述                   |
|------|--------------|---------|---------|------------------------|
| 0    | REPORT_ID    | uint8_t | -       | ReportID               |
| 1    | HDG_EC_L     | uint8_t | Bit 0   | 航向编码器左转                |
| 1    | HDG_EC_R     | uint8_t | Bit 1   | 航向编码器右转                |
| 1    | HDG_EC_SW    | uint8_t | Bit 2   | 航向编码器按下                |
| 1    | NOSE_DOWN    | uint8_t | Bit 3   | 垂直编码器上拨                |
| 1    | NOSE_UP      | uint8_t | Bit 4   | 垂直编码器下拨                |
| 1    | ALT_EC_L     | uint8_t | Bit 5   | 高度编码器左转                |
| 1    | ALT_EC_R     | uint8_t | Bit 6   | 高度编码器右转                |
| 1    | ALT_EC_SW    | uint8_t | Bit 7   | 高度编码器按下                |
| 2    | HDG          | uint8_t | Bit 0   | 航向保持按键                 |
| 2    | APR          | uint8_t | Bit 1   | 进近按键                   |
| 2    | NAV          | uint8_t | Bit 2   | 导航按键                   |
| 2    | TRK          | uint8_t | Bit 3   | 航迹按键                   |
| 2    | AP           | uint8_t | Bit 4   | 自动驾驶按键                 |
| 2    | FD           | uint8_t | Bit 5   | 飞行指引按键                 |
| 2    | LVL          | uint8_t | Bit 6   | 高度层改变按键，如果没有，可绑定FCTL按键 |
| 2    | YD           | uint8_t | Bit 7   | 偏航阻尼器按键                |
| 3    | IAS          | uint8_t | Bit 0   | 空速按键                   |
| 3    | VNAV         | uint8_t | Bit 1   | 垂直导航按键                 |
| 3    | VS           | uint8_t | Bit 2   | 垂直速率保持按键               |
| 3    | ALT          | uint8_t | Bit 3   | 高度保持按键                 |
| 3    | Reserved     | uint8_t | Bit 4-7 | (保留)                   |
| 4    | Light Sensor | uint8_t | -       | 环境光传感器，取值范围0-128       |

### 结构示意图

```
Byte 0: [REPORT_ID]
Byte 1: [ALT_EC_SW][ALT_EC_R][ALT_EC_L][NOSE_UP][NOSE_DOWN][HDG_EC_SW][HDG_EC_R][HDG_EC_L]
Byte 2: [YD][LVL][FD][AP][TRK][NAV][APR][HDG]
Byte 3: [Reserved][Reserved][Reserved][Reserved][ALT][VS][VNAV][IAS]
```

## OUTPUT 输出报告

**REPORT_ID = 2**

由电脑输出到设备。

### 报告总长度

64 字节

### 报告描述

箭头指示灯：亮起值=1，熄灭值=0。

| 字节索引 | 功能名称                 | 数据类型    | 位域      | 功能描述                       |
|------|----------------------|---------|---------|----------------------------|
| 0    | REPORT_ID            | uint8_t | -       | ReportID                   |
| 1    | Method               | uint8_t | -       | 请求方法，目前定义：1=DAP灯光，2=扩展面板灯光 |
| 2    | APR LED              | uint8_t | Bit 0   | APR 箭头指示灯                  |
| 2    | NAV LED              | uint8_t | Bit 1   | NAV 箭头指示灯                  |
| 2    | TRK LED              | uint8_t | Bit 2   | TRK 箭头指示灯                  |
| 2    | HDG LED              | uint8_t | Bit 3   | HDG 箭头指示灯                  |
| 2    | AP LED               | uint8_t | Bit 4   | AP 箭头指示灯                   |
| 2    | FD LED               | uint8_t | Bit 5   | FD 箭头指示灯                   |
| 2    | LVL LED              | uint8_t | Bit 6   | LVL 箭头指示灯                  |
| 2    | YD LED               | uint8_t | Bit 7   | YD 箭头指示灯                   |
| 3    | IAS LED              | uint8_t | Bit 0   | IAS 箭头指示灯                  |
| 3    | VNAV LED             | uint8_t | Bit 1   | VNAV 箭头指示灯                 |
| 3    | VS LED               | uint8_t | Bit 2   | VS 箭头指示灯                   |
| 3    | ALT LED              | uint8_t | Bit 3   | ALT 箭头指示灯                  |
| 3    | Reserved             | uint8_t | Bit 4-7 | (保留)                       |
| 4    | Backlight Brightness | uint8_t | -       | 背光亮度(值: 0-255)             |
| 5~63 | Reserved             | uint8_t | -       | (保留)                       |

### 结构示意图

```
Byte 0:  [REPORT_ID]
Byte 1:  [Method]
Byte 2:  [YD][LVL][FD][AP][HDG][TRK][NAV][APR]
Byte 3:  [Reserved][Reserved][Reserved][Reserved][ALT][VS][VNAV][IAS]
Byte 4:  [Backlight Brightness]
Byte 5~63:  [Reserved]
```