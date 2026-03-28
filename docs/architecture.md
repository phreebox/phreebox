# Architecture Overview

---

## System Architecture

Phreebox consists of two physical devices connected by a single USB-C cable.

```
┌──────────────────────────────────────────────────────┐
│                      CUBE                            │
│                                                      │
│  ┌────────────┐  ┌──────────┐  ┌─────────────────┐  │
│  │  Compute   │  │  Power   │  │    Wireless     │  │
│  │  Module    │  │  Module  │  │    Module       │  │
│  │ x86 CPU    │  │ Battery  │  │  WiFi / BT      │  │
│  │ RAM / NVMe │  │ Charging │  │  Open drivers   │  │
│  └────────────┘  └──────────┘  └─────────────────┘  │
│                                                      │
│              Arch Linux (standard)                   │
│              Wayland compositor                      │
│                                                      │
└───────────────────────┬──────────────────────────────┘
                        │
                     USB-C
                  (Phreebox Protocol v1)
                        │
┌───────────────────────┴──────────────────────────────┐
│                      PHONE                           │
│                                                      │
│  ┌────────────┐  ┌──────────┐  ┌─────────────────┐  │
│  │  Display   │  │  Radio   │  │    Camera       │  │
│  │  Module    │  │  Module  │  │    Module       │  │
│  │ Screen+    │  │  4G/5G   │  │  UVC stream     │  │
│  │ Touch      │  │  Modem   │  │  to Cube        │  │
│  └────────────┘  └──────────┘  └─────────────────┘  │
│                                                      │
│              Phone OS (minimal)                      │
│              USB gadget stack                        │
│                                                      │
└──────────────────────────────────────────────────────┘
```

---

## What the Cube Does

The Cube is a standard x86_64 PC running Arch Linux.

From the operating system's perspective, it has:
- A monitor (the Phone display, via DisplayPort Alt Mode)
- A USB HID input device (the Phone touch and buttons)
- A USB audio device (the Phone speaker and microphone)
- A USB network adapter (the Phone modem, via CDC-ECM)
- Several USB cameras (the Phone cameras, via UVC)

No custom drivers are needed on the Cube. Every component appears as a standard Linux device.

The user interacts with a full Wayland desktop on the Cube,
rendered on the Phone screen, controlled by Phone touch input.

---

## What the Phone Does

The Phone runs a minimal Linux system whose only job is:
- Drive the display (receive DisplayPort signal, show it)
- Forward touch input to the Cube (USB HID gadget)
- Share the modem connection (USB CDC-ECM gadget)
- Stream camera data (USB UVC gadget)
- Pass audio (USB Audio Class gadget)

The Phone does not run applications. It does not store user data.
It is a peripheral, not a computer.

---

## Software Stack

### Cube
```
Arch Linux (standard, unmodified)
  └── Wayland compositor (Sway or Plasma Wayland)
       └── Standard user applications
```

### Phone
```
Minimal Linux (custom, based on Arch Linux ARM or Alpine)
  ├── USB gadget stack (configfs)
  │   ├── HID gadget (touch + buttons)
  │   ├── UVC gadget (cameras)
  │   ├── UAC2 gadget (audio)
  │   └── CDC-ECM gadget (modem network)
  ├── ModemManager (4G/5G management)
  └── Minimal display driver (receives DP signal)
```

### Bridge Daemon
A small daemon (`phreebox-bridge`) runs on the Cube.
It monitors connection state, handles reconnection,
and exposes a status interface to the desktop.

---

## Key Design Decisions

### Why USB-C and not WiFi?
USB-C provides zero-configuration DisplayPort output.
No latency. No compression artifacts. No wireless interference.
WiFi mode is a future option (see `spec/rfcs/`), not the primary path.

### Why x86 and not ARM for the Cube?
Full Arch Linux package compatibility without recompilation.
Mature open-source driver ecosystem.
No vendor blobs required.
The performance and software ecosystem trade-offs strongly favour x86 for the compute unit.

### Why not put the compute in the phone?
Because phone-class SoCs (Qualcomm, MediaTek) have closed firmware,
locked bootloaders, and limited mainline kernel support.
Routing around the problem is cleaner than fighting it.

### Why Arch Linux?
Rolling release. User-controlled. No decisions made for you.
Consistent with the project philosophy.
The Cube is your computer. It runs what you tell it to run.
