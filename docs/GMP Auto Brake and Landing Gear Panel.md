# GMP自动刹车与起落架面板 HID 协议文档

> 由 WINGFLEX 量产工具自动生成
> 协议格式版本: 1.0

# 产品特点
GMP 是完全支持通用控制协议的产品。具有以下特点：

1. 支持游戏内直接绑定按键或轴数据输入。
2. 支持几乎所有语言快捷接入开发。
3. INPUT 报告仅在数据更新时上报。
4. FEATURE 报告下发便会保持设备灯光状态，自动待机时间可自行设置。

# 设计规范

1. 按键和轴使用 HID 通用 INPUT 协议，映射为JoyStick 的 Axis 和 Button，用户可自行绑定，游戏内可以识别。
2. 按键灯光使用 HID 自定义 FEATURE 协议，由上位机控制。

# PID & VID
vid: 0xC687
pid: 0xB217

## 输入按键报告

**基本信息**

| 属性 | 值 |
|------|-----|
| 方向 | INPUT |
| Report ID | 0x01 |
| 长度 | 8 字节 |
| Report ID 占用 [0] 字节 | 是 |

**字段定义**

| 字节 | 位 | 位长 | 类型 | 名称 | 描述 | 取值范围 | 默认值 |
|------|-----|------|------|------|------|----------|--------|
| 1 | 0 | 1 | bool | Brake Fan Key | 刹车风扇 [0=松开, 1=按下] | 0~1 |  |
| 1 | 1 | 1 | bool | AutoBrake Low Key | 自动刹车 Low 挡 [0=松开, 1=按下] | 0~1 | false |
| 1 | 2 | 1 | bool | AutoBrake Medium Key | 自动刹车 Medium 挡 [0=松开, 1=按下] | 0~1 | false |
| 1 | 3 | 1 | bool | AutoBrake Max Key | 自动刹车 Max 挡 [0=松开, 1=按下] | 0~1 | false |
| 1 | 4 | 1 | bool | Terrain On ND Key | 在ND显示地形按键 [0=松开, 1=按下] | 0~1 | false |
| 1 | 5 | 1 | bool | Anti Skid Switch | 防滑电门 [0=OFF, 1=ON] | 0~1 |  |
| 1 | 6 | 1 | bool | RST Encoder Left | RST 编码器左转 [0=OFF, 1=ON] | 0~1 |  |
| 1 | 7 | 1 | bool | RST Encoder Right | RST 编码器右转 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 0 | 1 | bool | RST Encoder Press | RST 编码器按下 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 1 | 1 | bool | CHR Encoder Left | CHR 编码器左转 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 2 | 1 | bool | CHR Encoder Right | CHR 编码器右转 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 3 | 1 | bool | CHR Encoder Press | CHR 编码器按下 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 4 | 1 | bool | SET Encoder Left | SET 编码器左转 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 5 | 1 | bool | SET Encoder Right | SET 编码器右转 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 6 | 1 | bool | SET Encoder Press | SET 编码器按下 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 7 | 1 | bool | 留空 | [0=OFF, 1=ON] | 保留 |  |
| 3 | 0 | 1 | bool | GPS1 | GPS旋钮挡位1 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 1 | 1 | bool | GPS2 | GPS旋钮挡位2 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 2 | 1 | bool | GPS3 | GPS旋钮挡位3 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 3 | 1 | bool | RUN1 | RUN旋钮挡位1 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 4 | 1 | bool | RUN2 | RUN旋钮挡位2 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 5 | 1 | bool | RUN3 | RUN旋钮挡位3 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 6 | 1 | bool | Landing Gear Handle Up | 起落架手柄收上 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 7 | 1 | bool | Landing Gear Handle Down | 起落架手柄放下 [0=OFF, 1=ON] | 0~1 |  |
| 4 | 0 | 16 | uint16 | Landing Gear Handle | 起落架手柄 | 0~1023 |  |
| 6 | 0 | 16 | uint16 | Light Sensor | 环境光传感器 | 0~127 |  |

## 灯光控制输出报告

**基本信息**

| 属性 | 值 |
|------|-----|
| 方向 | FEATURE_OUT |
| Report ID | 0x02 |
| 长度 | 34 字节 |
| Report ID 占用 [0] 字节 | 是 |

**字段定义**

| 字节 | 位 | 位长 | 类型 | 名称 | 描述 | 取值范围 | 默认值 |
|------|-----|------|------|------|------|----------|--------|
| 1 | 0 | 1 | bool | LDG Gear 1 UNLK | 起落架状态指示灯 [0=关闭, 1=打开] | 0~1 | false |
| 1 | 1 | 1 | bool | LDG Gear 1 Arrow | 起落架状态指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 1 | 2 | 1 | bool | LDG Gear 2 UNLK | 起落架状态指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 1 | 3 | 1 | bool | LDG Gear 2 Arrow | 起落架状态指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 1 | 4 | 1 | bool | LDG Gear 3 UNLK | 起落架状态指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 1 | 5 | 1 | bool | LDG Gear 3 Arrow | 起落架状态指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 1 | 6 | 1 | bool | Brake Fan HOT | 刹车风扇按键指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 1 | 7 | 1 | bool | Brake Fan ON | 刹车风扇按键指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 2 | 0 | 1 | bool | AutoBrk Low DECEL | 自动刹车指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 2 | 1 | 1 | bool | AutoBrk Low ON | 自动刹车指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 2 | 2 | 1 | bool | AutoBrk Med DECEL | 自动刹车指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 2 | 3 | 1 | bool | AutoBrk Med ON | 自动刹车指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 2 | 4 | 1 | bool | AutoBrk Max DECEL | 自动刹车指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 2 | 5 | 1 | bool | AutoBrk Max ON | 自动刹车指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 2 | 6 | 1 | bool | TERR ON ND ON | 地形显示指示灯 [0=关闭, 1=打开] | 0~1 |  |
| 2 | 7 | 1 | bool | Gear Red Arrow | 起落架手柄红色箭头灯 [0=关闭, 1=打开] | 0~1 |  |
| 3 | 0 | 8 | uint8 | Backlight Brightness | 背光灯亮度 | 0~255 | 128 |
| 4 | 0 | 8 | uint8 | Key Light Brightness | 按键指示灯亮度 | 0~255 | 128 |
| 5 | 0 | 8 | uint8 | Screen Brightness | 屏幕亮度 | 0~255 | 128 |
| 6 | 0 | 1 | bool | Cold And Dark | 冷舱模式，1=关闭所有灯光电源，忽略所有灯光指令，0=正常工作模式 | 0~1 | false |
| 6 | 1 | 1 | bool | ANN LT Test | 灯光测试模式，1=亮起所有按键指示灯光和数码管灯光，忽略所有灯光指令，0=正常工作模式（默认值） | 0~1 | false |
| 6 | 2 | 1 | bool | Clock Mode | 时钟模式设置 [0=直接控制模式, 1=桌面时钟模式] | 0~1 | false |
| 6 | 3 | 1 | bool | CHR Colon | CHR 计时器冒号 [0=关闭, 1=打开] | 0~1 | false |
| 6 | 4 | 1 | bool | UTC Colon Left | UTC 时钟冒号左 [0=关闭, 1=打开] | 0~1 | false |
| 6 | 5 | 1 | bool | UTC Colon Right | UTC 时钟冒号右 [0=关闭, 1=打开] | 0~1 | false |
| 6 | 6 | 1 | bool | ET Colon | ET 时钟冒号 [0=关闭, 1=打开] | 0~1 | false |
| 6 | 7 | 1 | bool | 保留 |  | 保留 |  |
| 7 | 0 | 8 | uint8 | Clock Brightness | 时钟亮度 | 0~8 | 4 |
| 8 | 0 | 8 | uint8 | CHR Digi 1 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 9 | 0 | 8 | uint8 | CHR Digi 2 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 10 | 0 | 8 | uint8 | CHR Digi 3 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 11 | 0 | 8 | uint8 | CHR Digi 4 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 12 | 0 | 8 | uint8 | UTC Digi 1 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 13 | 0 | 8 | uint8 | UTC Digi 2 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 14 | 0 | 8 | uint8 | UTC Digi 3 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 15 | 0 | 8 | uint8 | UTC Digi 4 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 16 | 0 | 8 | uint8 | UTC Digi 5 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 17 | 0 | 8 | uint8 | UTC Digi 6 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 18 | 0 | 8 | uint8 | ET Digi 1 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 19 | 0 | 8 | uint8 | ET Digi 2 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 20 | 0 | 8 | uint8 | ET Digi 3 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 21 | 0 | 8 | uint8 | ET Digi 4 | 取值0-9=数字0-9，0xA=短横线，0xF=不亮 |  | 15 |
| 22 | 0 | 16 | uint16 | BRAKE PRESS Left | 刹车压力左 | 0~3000 | 1000 |
| 24 | 0 | 16 | uint16 | BRAKE PRESS Right | 刹车压力右 | 0~3000 | 1000 |
| 26 | 0 | 16 | uint16 | ACCU PRESS | 制动蓄压器内的压力值 | 0~4000 | 3500 |
| 28 | 0 | 16 | uint16 | 保留 |  | 保留 |  |
| 30 | 0 | 32 | uint32 | Timestamp | 10位数字当地时间秒数，用于桌面时钟模式 |  | 1782835200 |

## 获取设备版本信息

获取固件和硬件版本信息

**基本信息**

| 属性 | 值 |
|------|-----|
| 方向 | FEATURE_IN |
| Report ID | 0x03 |
| 长度 | 11 字节 |
| Report ID 占用 [0] 字节 | 是 |

**字段定义**

| 字节 | 位 | 位长 | 类型 | 名称 | 描述 | 取值范围 | 默认值 |
|------|-----|------|------|------|------|----------|--------|
| 1 | 0 | 8 | uint8 | AutoBrk Status | 自动刹车面板设备状态 |  |  |
| 2 | 0 | 8 | uint8 | AutoBrk Hardware Version | 自动刹车面板硬件版本号 |  |  |
| 3 | 0 | 8 | uint8 | AutoBrk Firmware Version Major | 固件版本号 格式：Major.Minor.Patch |  |  |
| 4 | 0 | 8 | uint8 | AutoBrk Firmware Version Minor | 固件版本号 格式：Major.Minor.Patch |  |  |
| 5 | 0 | 8 | uint8 | AutoBrk Firmware Version Patch | 固件版本号 格式：Major.Minor.Patch |  |  |
| 6 | 0 | 8 | uint8 | Gear Status | 起落架面板设备状态 |  |  |
| 7 | 0 | 8 | uint8 | Gear Hardware Version | 起落架面板硬件版本号 |  |  |
| 8 | 0 | 8 | uint8 | Gear Firmware Version Major | 固件版本号 格式：Major.Minor.Patch |  |  |
| 9 | 0 | 8 | uint8 | Gear Firmware Version Minor | 固件版本号 格式：Major.Minor.Patch |  |  |
| 10 | 0 | 8 | uint8 | Gear Firmware Version Patch | 固件版本号 格式：Major.Minor.Patch |  |  |

## 特殊模式

**基本信息**

| 属性 | 值 |
|------|-----|
| 方向 | FEATURE_OUT |
| Report ID | 0x05 |
| 长度 | 3 字节 |
| Report ID 占用 [0] 字节 | 是 |

**字段定义**

| 字节 | 位 | 位长 | 类型 | 名称 | 描述 | 取值范围 | 默认值 |
|------|-----|------|------|------|------|----------|--------|
| 1 | 0 | 8 | enum | Hall Calibration Mode | 霍尔校准模式 [0=退出校准模式, 1=进入校准模式] |  | 0 |
| 2 | 0 | 8 | enum | Upgrade Mode | 升级模式，设置后设备将会重启进入升级模式 [0=正常启动, 1=升级模式] |  | 0 |

## 读取设备配置

**基本信息**

| 属性 | 值 |
|------|-----|
| 方向 | FEATURE_IN |
| Report ID | 0x04 |
| 长度 | 4 字节 |
| Report ID 占用 [0] 字节 | 是 |

**字段定义**

| 字节 | 位 | 位长 | 类型 | 名称 | 描述 | 取值范围 | 默认值 |
|------|-----|------|------|------|------|----------|--------|
| 1 | 0 | 16 | uint16 | Auto Standby Time | 自动待机时间，设备将在指定秒数后关闭灯光以节省电源 | 0~65535 | 5 |
| 3 | 0 | 8 | enum | Light Sensor Report Enabled | 是否开启环境光传感器上报 [0=禁用, 1=开启] |  | 1 |

## 写入设备配置

**基本信息**

| 属性 | 值 |
|------|-----|
| 方向 | FEATURE_OUT |
| Report ID | 0x04 |
| 长度 | 4 字节 |
| Report ID 占用 [0] 字节 | 是 |

**字段定义**

| 字节 | 位 | 位长 | 类型 | 名称 | 描述 | 取值范围 | 默认值 |
|------|-----|------|------|------|------|----------|--------|
| 1 | 0 | 16 | uint16 | Auto Standby Time | 自动待机时间，设备将在指定秒数后关闭灯光以节省电源 | 0~65535 | 5 |
| 3 | 0 | 8 | enum | Light Sensor Report Enabled | 是否开启环境光传感器上报 [0=禁用, 1=开启] |  | 1 |

## 读取按键状态

**基本信息**

| 属性 | 值 |
|------|-----|
| 方向 | FEATURE_IN |
| Report ID | 0x06 |
| 长度 | 8 字节 |
| Report ID 占用 [0] 字节 | 是 |

**字段定义**

| 字节 | 位 | 位长 | 类型 | 名称 | 描述 | 取值范围 | 默认值 |
|------|-----|------|------|------|------|----------|--------|
| 1 | 0 | 1 | bool | Brake Fan Key | 刹车风扇 [0=松开, 1=按下] | 0~1 |  |
| 1 | 1 | 1 | bool | AutoBrake Low Key | 自动刹车 Low 挡 [0=松开, 1=按下] | 0~1 | false |
| 1 | 2 | 1 | bool | AutoBrake Medium Key | 自动刹车 Medium 挡 [0=松开, 1=按下] | 0~1 | false |
| 1 | 3 | 1 | bool | AutoBrake Max Key | 自动刹车 Max 挡 [0=松开, 1=按下] | 0~1 | false |
| 1 | 4 | 1 | bool | Terrain On ND Key | 在ND显示地形按键 [0=松开, 1=按下] | 0~1 | false |
| 1 | 5 | 1 | bool | Anti Skid Switch | 防滑电门 [0=OFF, 1=ON] | 0~1 |  |
| 1 | 6 | 1 | bool | RST Encoder Left | RST 编码器左转 [0=OFF, 1=ON] | 0~1 |  |
| 1 | 7 | 1 | bool | RST Encoder Right | RST 编码器右转 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 0 | 1 | bool | RST Encoder Press | RST 编码器按下 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 1 | 1 | bool | CHR Encoder Left | CHR 编码器左转 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 2 | 1 | bool | CHR Encoder Right | CHR 编码器右转 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 3 | 1 | bool | CHR Encoder Press | CHR 编码器按下 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 4 | 1 | bool | SET Encoder Left | SET 编码器左转 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 5 | 1 | bool | SET Encoder Right | SET 编码器右转 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 6 | 1 | bool | SET Encoder Press | SET 编码器按下 [0=OFF, 1=ON] | 0~1 |  |
| 2 | 7 | 1 | bool | 留空 | [0=OFF, 1=ON] | 保留 |  |
| 3 | 0 | 1 | bool | GPS1 | GPS旋钮挡位1 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 1 | 1 | bool | GPS2 | GPS旋钮挡位2 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 2 | 1 | bool | GPS3 | GPS旋钮挡位3 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 3 | 1 | bool | RUN1 | RUN旋钮挡位1 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 4 | 1 | bool | RUN2 | RUN旋钮挡位2 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 5 | 1 | bool | RUN3 | RUN旋钮挡位3 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 6 | 1 | bool | Landing Gear Handle Up | 起落架手柄收上 [0=OFF, 1=ON] | 0~1 |  |
| 3 | 7 | 1 | bool | Landing Gear Handle Down | 起落架手柄放下 [0=OFF, 1=ON] | 0~1 |  |
| 4 | 0 | 16 | uint16 | Landing Gear Handle | 起落架手柄 | 0~1023 |  |
| 6 | 0 | 16 | uint16 | Light Sensor | 环境光传感器 | 0~127 |  |

