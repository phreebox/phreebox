# Connection Modes Specification

Phreebox supports three connection modes between Cube and Phone.

## Modes

### 1. Embedded
Cube physically inside Phone chassis.
No cable needed.

### 2. USB-C Wired  
Cube connected via USB-C cable.
Low latency, stable.

### 3. WiFi Direct (Wireless)
Cube and Phone connect peer-to-peer via WiFi Direct.
No router needed.
Cube can be at home while Phone is portable.

## Wireless Bridge Protocol

- Display: H264/AV1 stream from Cube to Phone
- Input: Touch/keyboard events from Phone to Cube  
- Transport: WiFi Direct + custom socket
- Latency target: <30ms

## Security

- End-to-end encrypted (WireGuard)
- Paired devices only
- Data never stored on Phone — always on Cube
