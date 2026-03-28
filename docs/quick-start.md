# Quick Start — First Prototype

This guide builds a working Phreebox proof of concept
using off-the-shelf hardware. No custom PCBs required.

**Goal:** Cube running Arch Linux, Phone screen showing Cube desktop,
touch input working, modem shared to Cube.

**Time:** 2–4 hours.
**Cost:** ~$150–200 depending on hardware you already own.

---

## Hardware Required

### For the Cube (pick one)
- **Recommended:** Intel N100 mini PC (Beelink Mini S12, GMKtec G3, or similar)
  - x86_64, 6W TDP, open graphics drivers, USB-C with DisplayPort
  - ~$100–130
- **Alternative:** Any x86_64 machine with USB-C DisplayPort output

### For the Phone
- **Recommended:** PinePhone Pro
  - Open hardware, mainline Linux kernel support, USB-C with DisplayPort output
  - ~$200
- **Alternative:** PinePhone (original) — slower but works
- **Not recommended for this guide:** Any Android phone (requires more setup)

### Other
- Full-featured USB-C cable (with E-Marker, supports DP Alt Mode)
- MicroSD card (16GB+) for PinePhone

---

## Step 1: Arch Linux on the Cube

Install standard Arch Linux on the mini PC.
Follow the official Arch installation guide: https://wiki.archlinux.org/title/Installation_guide

Install a Wayland compositor:
```bash
pacman -S sway swaybar swaybg swaylock
# or
pacman -S plasma-wayland-session
```

Verify DisplayPort output works by connecting a monitor via USB-C.

---

## Step 2: Minimal OS on the PinePhone

Download and flash Arch Linux ARM for PinePhone:
```
https://github.com/dreemurrs-embedded/Pine64-Arch/releases
```

Flash to MicroSD:
```bash
# Replace /dev/sdX with your SD card device
sudo dd if=archlinux-pinephone-pro-YYYYMMDD.img of=/dev/sdX bs=4M status=progress
sync
```

Boot PinePhone from MicroSD.

---

## Step 3: Configure USB Gadget on PinePhone

SSH into PinePhone (connect via WiFi or USB serial):

```bash
# Install required packages
pacman -S linux-megi usb-gadget-utils

# Enable gadget configuration on boot
systemctl enable phreebox-gadget
```

For this prototype, we configure manually:
```bash
# Load gadget modules
modprobe libcomposite

# Configure USB gadget (DisplayPort passthrough + HID + network)
/usr/share/phreebox/scripts/setup-gadget.sh
```

---

## Step 4: Connect

1. Connect PinePhone to mini PC via USB-C cable.
2. PinePhone screen should show the Cube desktop within 5 seconds.
3. Touch the PinePhone screen — cursor should move on the desktop.

If it does not work immediately, check:
```bash
# On Cube — check what USB devices appeared
lsusb
dmesg | tail -30

# Verify display output
swaymsg -t get_outputs
```

---

## What You Have

At this point you have a working Phreebox prototype.
It is not pretty. The software is rough. The hardware is bulky.

But the concept is proven:
- Full Arch Linux desktop running on x86
- Displayed on a phone screen
- Controlled by touch input
- Network shared from phone modem

This is the foundation everything else is built on.

---

## Next Steps

- `docs/porting-guide.md` — add support for a different phone
- `hardware/cube/` — build a proper Cube with modular hardware
- `hardware/phone/` — design a minimal phone board
- `software/bridge/` — contribute to the bridge daemon
