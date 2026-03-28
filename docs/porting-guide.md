# Porting Guide — Adding a New Phone

This guide explains how to add support for a new phone as a Phreebox Phone device.

---

## Requirements for a Compatible Phone

A phone can be a Phreebox Phone if it satisfies:

1. **Mainline Linux kernel support** (or very close to it)
   - Check: https://github.com/torvalds/linux — search for your SoC
   - Partial mainline support is acceptable if USB gadget stack works

2. **USB-C with DisplayPort Alt Mode**
   - The phone must be able to output DisplayPort over USB-C
   - Verify: does the phone work with a USB-C to DisplayPort adapter?

3. **USB gadget mode capable**
   - The phone's USB controller must support device/gadget mode
   - Most phones do. Verify in kernel config: `CONFIG_USB_GADGET=y`

4. **Open bootloader or unlockable**
   - You must be able to boot a custom kernel

---

## Porting Steps

### 1. Verify hardware requirements
Connect your phone to a monitor with USB-C to DisplayPort.
If the phone display mirrors to the monitor — DisplayPort Alt Mode works.

### 2. Get a working Linux environment on the phone
Options:
- PostmarketOS: https://postmarketos.org/devices/
- Arch Linux ARM: check community ports
- Build from scratch with Buildroot

Minimum working state: boots to shell, USB works.

### 3. Enable USB gadget stack
```bash
# Verify gadget support
zcat /proc/config.gz | grep USB_GADGET
# Should show: CONFIG_USB_GADGET=y

# Load modules
modprobe libcomposite
modprobe usb_f_hid
modprobe usb_f_uac2
modprobe usb_f_ecm
modprobe usb_f_uvc
```

### 4. Run the gadget setup script
```bash
git clone https://github.com/phreebox/phreebox
cd phreebox
./scripts/setup-gadget.sh
```

If this fails, open an issue with the error output and your phone model.

### 5. Document your port

Create `community/builds/<manufacturer>-<model>/`:
```
community/builds/pine64-pinephone-pro/
├── README.md          (status, known issues, build instructions)
├── kernel-config      (diff from mainline config)
└── notes.md           (anything unusual about this device)
```

### 6. Submit

Open a pull request. Title: `[port] Manufacturer Model Name`

---

## Known Working Devices

| Device              | Status    | Maintainer  | Notes                        |
|---------------------|-----------|-------------|------------------------------|
| PinePhone Pro       | tested    | core team   | Reference device             |
| PinePhone (orig.)   | tested    | core team   | Works, slower CPU            |

---

## Known Non-Working Devices

| Device              | Blocker                              |
|---------------------|--------------------------------------|
| Most Qualcomm phones | Closed GPU/modem firmware, no DP Alt Mode via mainline |
| iPhone              | Closed everything                    |
