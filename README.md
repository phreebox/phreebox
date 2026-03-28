# Phreebox

> *Your phone is a computer. It should belong to you.*

Phreebox is an open hardware and software platform that separates the **compute** from the **display** in a mobile device.

A small cube runs full desktop Arch Linux on x86 hardware.
A phone becomes a portable screen, touch surface, and radio module.
Everything is modular. Everything is documented. Everything is yours.

---

## How It Works

```
┌─────────────────────┐         ┌──────────────────────┐
│        CUBE         │         │        PHONE         │
│  x86_64 CPU         │◄───────►│  Display module      │
│  Arch Linux         │  USB-C  │  Touch input         │
│  Open drivers       │         │  4G/5G modem         │
│  User-owned         │         │  Camera, Battery     │
└─────────────────────┘         └──────────────────────┘
```

The Cube is a standard PC. Every Arch Linux package works, out of the box.
The Phone is a thin client — screen, input, and radio. Nothing more.

---

## Repository Structure

```
phreebox/
├── spec/               Protocol and form-factor specifications
├── hardware/           Schematics and module designs (KiCad)
│   ├── cube/           Cube modules: compute, power, wireless, expansion
│   └── phone/          Phone modules: display, radio, camera, battery
├── software/           
│   ├── cube-os/        Arch Linux configuration and packages for the Cube
│   ├── phone-os/       Minimal OS for the Phone (display client)
│   └── bridge/         Daemon that connects Cube and Phone
├── community/          Community-contributed modules and builds
├── docs/               Guides, architecture docs, porting instructions
└── scripts/            Build and flash utilities
```

---

## Getting Started

→ Read [PHILOSOPHY.md](./PHILOSOPHY.md) to understand why this exists.
→ Read [docs/architecture.md](./docs/architecture.md) for the technical overview.
→ Read [docs/quick-start.md](./docs/quick-start.md) to build your first prototype.
→ Read [CONTRIBUTING.md](./CONTRIBUTING.md) to add your own module.

---

## Licenses

| Layer         | License                        |
|---------------|--------------------------------|
| Hardware      | CERN Open Hardware License v2  |
| Software      | GNU General Public License v3  |
| Specification | CC-BY-SA 4.0                   |
| Documentation | CC-BY-SA 4.0                   |

---

## Status

🔧 **Early development.** Specification in progress. First prototype not yet built.

This is the right time to contribute to the spec and architecture decisions
before they become hard to change.
