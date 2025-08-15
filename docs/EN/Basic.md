# Basic Section

## Introduction to Device Communication Principles

WINGFLEXSIM devices use USB HID to send custom reports for communication functions. Most of the device's functionality is designed to be "stateless," which means that throughout the entire communication process, the device's state is completely determined by the host software.
As long as the host continuously sends the latest status data to the device, the device will always remain synchronized with the host status.

### Data Rate, Frame Size

The device periodically uploads key input data (1kHz), with 64 Bytes per frame.

The connection software needs to periodically send messages to the device, such as light signals, etc. Recommended frequency: 1kHz, 64 Bytes per frame. (Some products have a feature that automatically turns off after 1-3 seconds without data input.)

### Data Definition

Each device has defined uplink and downlink data.

- Uplink data: Data sent from the device to the computer.
- Downlink data: Data sent from the computer to the device.

Let `Uint8 Bytes[64]` be the array for uplink data. The data structure of uplink data is as follows:

- `Bytes[0]-[2]`: Fixed message header bytes of the device, with a length of 3 bytes. The specific values are defined in the protocol of each device.
- `Bytes[3]`: How many types of data are included in this data transmission.
  - In the protocol documentation, this is referred to as "Data Type".
  - There can be up to 3 different types. If this transmission contains 1 type of data, the value is 0x01; if it contains 3 types, the value is 0x03. A single transmission can consist of bit-type, single-byte type, and double-byte type data.
- `Bytes[4]`: Type declaration byte, indicating the data type of the following bytes.
  - In the protocol documentation, this is referred to as "Data Type". If this transmission contains 3 types of data, this "Data Type" declaration byte will appear three times.
  - Values: bit-type (0x01), single-byte type (0x02), double-byte type (0x03).
- `Bytes[5]`: Data length declaration byte for this type, in bytes.
  - In the protocol documentation, this is referred to as "Data Length".
  - For example, if followed by 1 byte of data representing 3 switch states using 3 bits, the length declaration byte value is 0x01.
  - Similarly, if followed by 3 bytes of data representing 20 switch states using 20 bits, the length declaration byte value is 0x03.
- `Bytes[6]-[n]`: Data bytes.
- `Bytes[n+1]`: "Data Type". If there is a second type of data, this indicates the type of the second data.
- `Bytes[n+2]`: "Data Length". If there is a second type of data, this indicates the number of bytes occupied by the second data.

The downlink data structure can be parsed with reference to the above description.

## Connection Example

Please use a browser to view the HTML page: `example/USB HID Connection Example.html`
