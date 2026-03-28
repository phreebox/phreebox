# phreebox-bridge

The bridge daemon runs on the Cube. It monitors the connection to the Phone
and manages the state of the system.

---

## What It Does

- Detects Phone connect/disconnect events
- Configures display output when Phone connects
- Notifies the desktop environment of Phone status
- Exposes a D-Bus interface for status queries
- Logs connection events

## What It Does NOT Do

- It does not handle display rendering (that is the Wayland compositor)
- It does not handle input (that is the kernel HID driver)
- It does not handle audio (that is PipeWire/PulseAudio)
- It does not handle networking (that is NetworkManager)

The bridge is intentionally minimal. The kernel and standard Linux userspace
handle everything they can handle. The bridge only fills the gaps.

---

## Building

```bash
cd software/bridge
make
```

Dependencies: libudev, libdbus-1, standard C library.
No other dependencies. Intentional.

---

## Installing

```bash
make install
systemctl enable --now phreebox-bridge
```

---

## D-Bus Interface

Service: `org.phreebox.Bridge`
Object: `/org/phreebox/Bridge`

Methods:
- `GetStatus() → (connected: bool, protocol_version: string)`
- `GetPhoneInfo() → (model: string, battery: int, signal: int)`

Signals:
- `PhoneConnected(protocol_version: string)`
- `PhoneDisconnected()`
