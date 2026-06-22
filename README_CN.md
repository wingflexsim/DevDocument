[English](README.md) | [中文](README_CN.md)

# WINGFLEXSIM 设备集成开发文档

本仓库提供将 WINGFLEXSIM 飞行模拟硬件集成到第三方软件所需的协议文档和示例。

- [官方网站](https://wingflexsim.com/)
- [反馈文档问题](https://github.com/wingflexsim/DevDocument/issues)

## 项目简介

本仓库介绍受支持的 WINGFLEXSIM 设备如何通过 USB HID 进行通信，适用于希望在飞行模拟软件或其他连接工具中添加 WINGFLEXSIM 设备支持的社区开发者、硬件供应商和爱好者。

仓库中的示例使用 JavaScript 和 HTML 编写，可在兼容的浏览器中直接测试设备通信。理解协议后，您可以使用任何支持 USB HID 的编程语言或框架完成集成。

## 快速开始

1. 阅读[通信基础](docs/CN/Basic.md)，了解报告、帧大小以及上行和下行数据。
2. 打开对应设备的协议文档。
3. 查看 [`examples/`](examples/) 中的 JavaScript/HTML 示例。
4. 根据您的应用程序和开发语言实现协议。

## 支持的设备文档

| 设备 | 文档 |
| --- | --- |
| A320 EFIS CUBE | [协议](docs/A320%20EFIS%20CUBE.md) |
| A320 FCU CUBE | [协议](docs/A320%20FCU%20CUBE.md) |
| A320 OVHD CUBE | [协议](docs/A320%20OVHD%20CUBE.md) |
| A320 RMP CUBE | [协议](docs/A320%20RMP%20CUBE.md) |
| DAP 500 | [English](docs/DAP%20500_EN.md) · [中文](docs/DAP%20500_CN.md) |

其他设备的文档将在协议完成编辑和测试后陆续添加。

## 仓库结构

```text
.
├── docs/
│   ├── EN/          # 英文通用文档
│   ├── CN/          # 中文通用文档
│   └── ...          # 设备协议文档
├── examples/        # 基于浏览器的 USB HID 示例
├── README.md        # 英文项目说明
└── README_CN.md     # 中文项目说明
```

## 参与贡献

如果您发现文档中存在错误、歧义或翻译问题，请[提交 Issue](https://github.com/wingflexsim/DevDocument/issues)。反馈协议问题时，请提供设备型号、相关字段或字节位置、预期行为以及实际观察到的行为。

## 免责声明

1. 本文档用于 WINGFLEXSIM 飞行模拟设备的非官方、非商业集成。
2. 完成设备集成并不代表获得 WINGFLEXSIM 的官方支持、认可、合作关系或商业授权。未经书面授权，请勿声称与 WINGFLEXSIM 存在上述关系。
3. 您有责任测试自己的实现。对于第三方软件或集成导致的问题，包括设备损坏、功能异常、连接不稳定、游戏性能下降或崩溃，WINGFLEXSIM 不承担责任。
4. 由于文档仍在持续开发，并涉及国际协作，内容可能存在错误、不准确之处或翻译问题。

