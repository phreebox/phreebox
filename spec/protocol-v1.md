# Phreebox Protocol v1

**Status:** Draft
**Version:** 1.0.0-draft
**Stability:** Unstable — do not build hardware against this yet

---

## Overview

The Phreebox Protocol defines the complete interface between the Cube and the Phone.
Any Cube-compatible device and any Phone-compatible device that implement this spec
must interoperate correctly.

This document is the contract. It does not specify implementation — only behaviour and interfaces.

---

## Physical Layer

### Connector
- **Primary:** USB-C (USB 3.2 Gen 2 minimum)
- **Alternate modes required:** DisplayPort 1.4 Alt Mode, USB Power Delivery 3.0
- **Cable requirement:** Full-featured USB-C cable (E-Marker required for >60W)

### Power
- Cube supplies power to Phone over USB-C PD.
- Negotiated voltage: 5V / 9V / 15V / 20V (Phone requests, Cube supplies).
- Minimum supply: 15W (5V@3A).
- Phone battery charges from Cube when connected.

---

## Display Channel

- **Transport:** DisplayPort 1.4 over USB-C Alt Mode
- **Maximum resolution:** 2560×1440 @ 120Hz
- **Minimum resolution:** 1080×1920 @ 60Hz (portrait)
- **Color depth:** 8-bit minimum, 10-bit optional
- **HDR:** Optional. Phone advertises capability via EDID.

The Phone exposes a standard DisplayPort sink.
The Cube drives it as a standard external monitor.
No special software is required on the Cube side for display output.

---

## Input Channel

Touch events and physical button events from the Phone are sent to the Cube
over the USB data channel as a standard USB HID device.

### Touch
- Protocol: USB HID Digitizer (Usage Page 0x0D)
- Multi-touch: minimum 10 simultaneous points
- Report rate: minimum 120Hz
- Coordinates: reported in display pixels, origin top-left

### Buttons
- Power button: HID Consumer Control (system power)
- Volume up/down: HID Consumer Control (volume)
- Custom buttons (if present): HID Generic Button

The Cube sees the Phone as a standard USB HID input device.
No driver is required beyond standard kernel HID support.

---

## Audio Channel

- **Transport:** USB Audio Class 2.0 over USB data channel
- **Output (Cube → Phone speaker):** 2-channel PCM, 48kHz, 16-bit minimum
- **Input (Phone microphone → Cube):** 1-channel PCM, 48kHz, 16-bit minimum
- The Phone appears as a standard USB audio device to the Cube.

---

## Network Channel (Modem Share)

The Phone shares its 4G/5G modem connection with the Cube.

- **Transport:** USB CDC-ECM (Ethernet over USB)
- The Phone acts as a USB network adapter (USB gadget mode).
- The Cube sees a standard Ethernet interface (e.g., `usb0`).
- The Phone handles NAT and DHCP internally.
- IP assignment: Phone assigns Cube an address in `192.168.42.0/24`.

This is the same mechanism used by USB tethering on Android.
Standard Linux kernel support. No custom driver needed on the Cube.

---

## Camera Channel

Camera data is streamed from the Phone to the Cube over USB.

- **Transport:** USB Video Class (UVC) 1.5
- The Phone exposes each camera as a standard UVC device.
- The Cube sees standard `/dev/video*` devices.
- Formats supported: MJPEG minimum; H.264 optional.
- Minimum resolution: 1080p @ 30fps

---

## State and Handshake

On USB-C connection:

1. Physical connection established. PD negotiation begins.
2. DisplayPort Alt Mode activated. Phone display turns on.
3. USB enumeration: Phone exposes HID, Audio, CDC-ECM, UVC interfaces.
4. Cube acquires network route through Phone modem (if modem active).
5. System is operational.

On disconnection:

1. Cube detects USB disconnect.
2. Cube suspends display output.
3. Phone switches to standalone mode (shows disconnect screen).
4. Phone OS continues running independently.

---

## Versioning

This protocol uses semantic versioning.

- **Major version bump:** breaking change. Existing hardware may not be compatible.
- **Minor version bump:** additive change. Backwards compatible.
- **Patch version bump:** clarification only. No behaviour change.

Devices advertise supported protocol version via USB descriptor string.
Cube and Phone negotiate the highest mutually supported version on connect.

---

## What This Spec Does NOT Define

- The internal implementation of the Phone OS
- The internal implementation of the Cube OS
- The physical form factor of either device (see `cube-form-factor.md`, `phone-form-factor.md`)
- The module interface within the Phone or Cube (see `module-interface.md`)

---

## RFC Process

Changes to this document require an RFC.
See `spec/rfcs/0000-template.md` and `CONTRIBUTING.md`.
