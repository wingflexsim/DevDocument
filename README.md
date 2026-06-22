[English](README.md) | [中文](README_CN.md)

# WINGFLEXSIM Device Integration Documentation

Documentation and examples for integrating WINGFLEXSIM flight-simulation hardware with third-party software.

- [Official website](https://wingflexsim.com/)
- [Report a documentation issue](https://github.com/wingflexsim/DevDocument/issues)

## Overview

This repository describes how supported WINGFLEXSIM devices communicate over USB HID. It is intended for community developers, hardware suppliers, and enthusiasts who want to add WINGFLEXSIM device support to flight-simulation software or other connection tools.

The included examples use JavaScript and HTML so that communication can be tested directly in a compatible browser. Once you understand the protocol, you can implement it in any language or framework with USB HID support.

## Getting Started

1. Read the [communication basics](docs/EN/Basic.md) to understand reports, frame sizes, and uplink/downlink data.
2. Open the protocol document for your device.
3. Review the files in [`examples/`](examples/) for a working JavaScript/HTML reference.
4. Adapt the protocol to your application and preferred programming language.

## Supported Device Documentation

| Device | Documentation |
| --- | --- |
| A320 EFIS CUBE | [Protocol](docs/A320%20EFIS%20CUBE.md) |
| A320 FCU CUBE | [Protocol](docs/A320%20FCU%20CUBE.md) |
| A320 OVHD CUBE | [Protocol](docs/A320%20OVHD%20CUBE.md) |
| A320 RMP CUBE | [Protocol](docs/A320%20RMP%20CUBE.md) |
| DAP 500 | [English](docs/DAP%20500_EN.md) · [中文](docs/DAP%20500_CN.md) |

Additional device documentation may be added as protocols are edited and tested.

## Repository Structure

```text
.
├── docs/
│   ├── EN/          # English general documentation
│   ├── CN/          # Chinese general documentation
│   └── ...          # Device protocol documents
├── examples/        # Browser-based USB HID examples
├── README.md        # English overview
└── README_CN.md     # Chinese overview
```

## Contributing

If you find an error, ambiguity, or translation issue, please [open an issue](https://github.com/wingflexsim/DevDocument/issues). When reporting a protocol problem, include the device model, the relevant field or byte position, the expected behavior, and the behavior you observed.

## Disclaimer

1. This documentation is provided for unofficial, non-commercial integration of WINGFLEXSIM flight-simulation devices.
2. An integration does not imply official support, endorsement, partnership, or commercial authorization from WINGFLEXSIM. Do not claim such a relationship without written authorization.
3. You are responsible for testing your implementation. WINGFLEXSIM is not responsible for issues arising from third-party software or integrations, including device damage, abnormal behavior, unstable connections, reduced game performance, or crashes.
4. The documentation may contain errors, inaccuracies, or translation mistakes due to ongoing development and international collaboration.
