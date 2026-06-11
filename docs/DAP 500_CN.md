# DAP 500 通讯协议

2026-06-03 更新

## 产品特点

DAP 500 这是完全支持通用控制协议的产品。具有以下特点：
1. 支持游戏内直接绑定按键或轴数据输入。
2. 支持几乎所有语言快捷接入开发。
3. INPUT 报告仅在数据更新时上报。
4. FEATURE 报告下发便会保持设备灯光状态，自动待机时间可自行设置。

## 设计规范

1. 按键和轴使用 HID 通用 INPUT 协议，映射为JoyStick 的 Axis 和 Button，用户可自行绑定，游戏内可以识别。
2. 按键灯光使用 HID 自定义 FEATURE 协议，由上位机控制。

## PID & VID

- VID: 0xC687
- PID: 0xB216

## INPUT 报告 id=1

**REPORT_ID = 1**

### 报告总长度

5 字节

### 功能描述

- 报告按键状态。
- 报告环境光传感器状态。

| 字节索引 | 功能名称         | 数据类型    | 位域      | 功能描述               |
|------|--------------|---------|---------|--------------------|
| 0    | REPORT_ID    | uint8_t | -       | ReportID           |
| 1    | HDG_EC_L     | uint8_t | Bit 0   | 航向编码器左转，按下=1，松开=0  |
| 1    | HDG_EC_R     | uint8_t | Bit 1   | 航向编码器右转，按下=1，松开=0  |
| 1    | HDG_EC_SW    | uint8_t | Bit 2   | 航向编码器按下，按下=1，松开=0  |
| 1    | NOSE_DOWN    | uint8_t | Bit 3   | 垂直编码器上拨，按下=1，松开=0  |
| 1    | NOSE_UP      | uint8_t | Bit 4   | 垂直编码器下拨，按下=1，松开=0  |
| 1    | ALT_EC_L     | uint8_t | Bit 5   | 高度编码器左转，按下=1，松开=0  |
| 1    | ALT_EC_R     | uint8_t | Bit 6   | 高度编码器右转，按下=1，松开=0  |
| 1    | ALT_EC_SW    | uint8_t | Bit 7   | 高度编码器按下，按下=1，松开=0  |
| 2    | HDG          | uint8_t | Bit 0   | 航向保持按键，按下=1，松开=0   |
| 2    | APR          | uint8_t | Bit 1   | 进近按键，按下=1，松开=0     |
| 2    | NAV          | uint8_t | Bit 2   | 导航按键，按下=1，松开=0     |
| 2    | TRK          | uint8_t | Bit 3   | 航迹按键，按下=1，松开=0     |
| 2    | AP           | uint8_t | Bit 4   | 自动驾驶按键，按下=1，松开=0   |
| 2    | FD           | uint8_t | Bit 5   | 飞行指引按键，按下=1，松开=0   |
| 2    | LVL          | uint8_t | Bit 6   | 高度层改变按键，按下=1，松开=0  |
| 2    | YD           | uint8_t | Bit 7   | 偏航阻尼器按键，按下=1，松开=0  |
| 3    | IAS          | uint8_t | Bit 0   | 空速按键，按下=1，松开=0     |
| 3    | VNAV         | uint8_t | Bit 1   | 垂直导航按键，按下=1，松开=0   |
| 3    | VS           | uint8_t | Bit 2   | 垂直速率保持按键，按下=1，松开=0 |
| 3    | ALT          | uint8_t | Bit 3   | 高度保持按键，按下=1，松开=0   |
| 3    | Reserved     | uint8_t | Bit 4-7 | (保留)               |
| 4    | Light Sensor | uint8_t | -       | 环境光传感器，取值范围0-128   |

### 结构示意图

```
Byte 0: [REPORT_ID]
Byte 1: [ALT_EC_SW][ALT_EC_R][ALT_EC_L][NOSE_UP][NOSE_DOWN][HDG_EC_SW][HDG_EC_R][HDG_EC_L]
Byte 2: [YD][LVL][FD][AP][TRK][NAV][APR][HDG]
Byte 3: [Reserved][Reserved][Reserved][Reserved][ALT][VS][VNAV][IAS]
Byte 4: [Light Sensor]
```

## Feature SET_REPORT 报告

**REPORT_ID = 2**

### 报告总长度

5 字节

### 功能描述

- 设置按键箭头指示灯。
- 设置背光灯亮度。

| 字节索引 | 功能名称                 | 数据类型    | 位域      | 功能描述                    |
|------|----------------------|---------|---------|-------------------------|
| 0    | REPORT_ID            | uint8_t | -       | ReportID                |
| 1    | APR LED              | uint8_t | Bit 0   | APR 箭头指示灯，开=1，关=0(默认)   |
| 1    | NAV LED              | uint8_t | Bit 1   | NAV 箭头指示灯，开=1，关=0(默认)   |
| 1    | TRK LED              | uint8_t | Bit 2   | TRK 箭头指示灯，开=1，关=0(默认)   |
| 1    | HDG LED              | uint8_t | Bit 3   | HDG 箭头指示灯，开=1，关=0(默认)   |
| 1    | AP LED               | uint8_t | Bit 4   | AP 箭头指示灯，开=1，关=0(默认)    |
| 1    | FD LED               | uint8_t | Bit 5   | FD 箭头指示灯，开=1，关=0(默认)    |
| 1    | LVL LED              | uint8_t | Bit 6   | LVL 箭头指示灯，开=1，关=0(默认)   |
| 1    | YD LED               | uint8_t | Bit 7   | YD 箭头指示灯，开=1，关=0(默认)    |
| 2    | IAS LED              | uint8_t | Bit 0   | IAS 箭头指示灯，开=1，关=0(默认)   |
| 2    | VNAV LED             | uint8_t | Bit 1   | VNAV 箭头指示灯，开=1，关=0(默认)  |
| 2    | VS LED               | uint8_t | Bit 2   | VS 箭头指示灯，开=1，关=0(默认)    |
| 2    | ALT LED              | uint8_t | Bit 3   | ALT 箭头指示灯，开=1，关=0(默认)   |
| 2    | Reserved             | uint8_t | Bit 4-7 | (保留)                    |
| 3    | Backlight Brightness | uint8_t | -       | 背光亮度(取值: 0-255) 默认值：255 |
| 4    | Reserved             | uint8_t | -       | (保留)                    |

### 结构示意图

```
Byte 0:  [REPORT_ID]
Byte 1:  [YD][LVL][FD][AP][HDG][TRK][NAV][APR]
Byte 2:  [Reserved][Reserved][Reserved][Reserved][ALT][VS][VNAV][IAS]
Byte 3:  [Reserved][Reserved][Reserved][Reserved][Reserved][Reserved][Reserved][Auto Backlight]
Byte 4:  [Backlight Brightness]
Byte 5-7:  [Reserved]
```

## Feature GET_REPORT id=2

**REPORT_ID = 2**

### 报告总长度

5 字节

## 功能描述

- 报告按键状态。
- 报告环境光状态。

| 字节索引 | 功能名称           | 数据类型    | 位域      | 功能描述                 |
|------|----------------|---------|---------|----------------------|
| 0    | REPORT_ID      | uint8_t | -       | ReportID             |
| 1    | HDG_EC_L       | uint8_t | Bit 0   | 航向编码器左转，按下=1，松开=0    |
| 1    | HDG_EC_R       | uint8_t | Bit 1   | 航向编码器右转，按下=1，松开=0    |
| 1    | HDG_EC_SW      | uint8_t | Bit 2   | 航向编码器按下，按下=1，松开=0    |
| 1    | NOSE_DOWN      | uint8_t | Bit 3   | 垂直编码器上拨，按下=1，松开=0    |
| 1    | NOSE_UP        | uint8_t | Bit 4   | 垂直编码器下拨，按下=1，松开=0    |
| 1    | ALT_EC_L       | uint8_t | Bit 5   | 高度编码器左转，按下=1，松开=0    |
| 1    | ALT_EC_R       | uint8_t | Bit 6   | 高度编码器右转，按下=1，松开=0    |
| 1    | ALT_EC_SW      | uint8_t | Bit 7   | 高度编码器按下，按下=1，松开=0    |
| 2    | HDG            | uint8_t | Bit 0   | 航向保持按键，按下=1，松开=0     |
| 2    | APR            | uint8_t | Bit 1   | 进近按键，按下=1，松开=0       |
| 2    | NAV            | uint8_t | Bit 2   | 导航按键，按下=1，松开=0       |
| 2    | TRK            | uint8_t | Bit 3   | 航迹按键，按下=1，松开=0       |
| 2    | AP             | uint8_t | Bit 4   | 自动驾驶按键，按下=1，松开=0     |
| 2    | FD             | uint8_t | Bit 5   | 飞行指引按键，按下=1，松开=0     |
| 2    | LVL            | uint8_t | Bit 6   | 高度层改变按键，按下=1，松开=0    |
| 2    | YD             | uint8_t | Bit 7   | 偏航阻尼器按键，按下=1，松开=0    |
| 3    | IAS            | uint8_t | Bit 0   | 空速按键，按下=1，松开=0       |
| 3    | VNAV           | uint8_t | Bit 1   | 垂直导航按键，按下=1，松开=0     |
| 3    | VS             | uint8_t | Bit 2   | 垂直速率保持按键，按下=1，松开=0   |
| 3    | ALT            | uint8_t | Bit 3   | 高度保持按键，按下=1，松开=0     |
| 3    | Reserved       | uint8_t | Bit 4-7 | (保留)                 |
| 4    | Light Sensor   | uint8_t | -       | 环境光传感器，取值范围0-128     |

### 结构示意图

```
Byte 0:  [REPORT_ID]
Byte 1:  [ALT_EC_SW][ALT_EC_R][ALT_EC_L][NOSE_UP][NOSE_DOWN][HDG_EC_SW][HDG_EC_R][HDG_EC_L]
Byte 2:  [YD][LVL][FD][AP][TRK][NAV][APR][HDG]
Byte 3:  [Reserved][Reserved][Reserved][Reserved][ALT][VS][VNAV][IAS]
Byte 4:  [Light Sensor]
```

## Feature GET_REPORT id=3

**REPORT_ID = 3**

### 报告总长度

5 字节

## 功能描述

- 报告硬件和固件版本号。

| 字节索引 | 功能名称             | 数据类型    | 位域 | 功能描述                   |
|------|------------------|---------|----|------------------------|
| 0    | REPORT_ID        | uint8_t | -  | ReportID               |
| 1    | HW Version       | uint8_t | -  | Hardware Version       |
| 2    | FW Version Major | uint8_t | -  | Firmware Version Major |
| 3    | FW Version Minor | uint8_t | -  | Firmware Version Minor |
| 4    | FW Version Patch | uint8_t | -  | Firmware Version Patch |

### 结构示意图

```
Byte 0: [REPORT_ID]
Byte 1: [HW Version]
Byte 2: [FW Version Major]
Byte 3: [FW Version Minor]
Byte 4: [FW Version Patch]
```

## Feature SET_REPORT id = 4

**REPORT_ID = 4**

### 报告总长度

5 字节

## 功能描述

- 报告自定义设置。

| 字节索引 | 功能名称                       | 数据类型     | 位域      | 功能描述                                            |
|------|----------------------------|----------|---------|-------------------------------------------------|
| 0    | REPORT_ID                  | uint8_t  | -       | ReportID                                        |
| 1    | Auto Backlight Enable      | uint8_t  | Bit 0   | 是否开启自动背光，开=1，关=0(默认)                            |
| 1    | Light Sensor Report Enable | uint8_t  | Bit 1   | 是否开启光传感器上报，开=1(默认)，关=0                          |
| 1    | Reserved                   | uint8_t  | Bit 2-7 | (保留)                                            |
| 2    | Reserved                   | uint8_t  | -       | (保留)                                            |
| 3-4  | Auto Standby Time          | uint16_t | -       | 自动待机时间(单位：秒)，无通讯指定时间后自动关闭灯光，默认值=5(sec)，最大值65535 |


## Feature GET_REPORT id = 4

**REPORT_ID = 4

### 报告总长度

5 字节

## 功能描述

- 报告自定义设置。

| 字节索引 | 功能名称                       | 数据类型     | 位域      | 功能描述                                            |
|------|----------------------------|----------|---------|-------------------------------------------------|
| 0    | REPORT_ID                  | uint8_t  | -       | ReportID                                        |
| 1    | Auto Backlight Enable      | uint8_t  | Bit 0   | 是否开启自动背光，开=1，关=0(默认)                            |
| 1    | Light Sensor Report Enable | uint8_t  | Bit 1   | 是否开启光传感器上报，开=1(默认)，关=0                          |
| 1    | Reserved                   | uint8_t  | Bit 2-7 | (保留)                                            |
| 2    | Reserved                   | uint8_t  | -       | (保留)                                            |
| 3-4  | Auto Standby Time          | uint16_t | -       | 自动待机时间(单位：秒)，无通讯指定时间后自动关闭灯光，默认值=5(sec)，最大值65535 |
