# Module Interface Specification

**Status:** Draft

---

## Purpose

This document defines what it means to be a Phreebox module.
Any hardware component that satisfies these requirements
can be used in a Phreebox Cube or Phone without modification to the rest of the system.

---

## Cube Module Interface

All Cube modules connect via a common internal bus.

### Physical
- Connector: M.2 E-key (for wireless/expansion) or custom Phreebox Cube Bus (PCB)
- Form factor: defined per module type in `hardware/cube/modules/<type>/README.md`
- Power rails available: 3.3V, 5V, 12V (from Power module)

### Electrical
- Each module must declare: max current draw per rail
- Each module must include: reverse polarity protection
- ESD protection: required on all external-facing pins

### Software
- Must work with mainline Linux kernel drivers only
- No out-of-tree kernel modules allowed in reference design
- Firmware (if any) must be open source and buildable from source

---

## Phone Module Interface

### Physical
- Connector: Phreebox Phone Bus (specification in `hardware/phone/reference-design/`)
- Modules connect via flat flex cable or direct PCB-to-PCB connector
- Each module is a separate PCB

### Electrical
- Power supplied by Battery module
- Each module declares max current draw

### Software
- Same rule: mainline Linux kernel only
- Phone OS must detect module presence via hardware ID pins

---

## What a Module README Must Contain

Every module in `hardware/` or `community/modules/` must include a `README.md` with:

1. **Purpose** — what this module does in one sentence
2. **Interface** — which bus it uses, which signals it exposes
3. **Power** — voltage rails used, max current draw
4. **BOM** — complete bill of materials with part numbers and sources
5. **Build instructions** — how to fabricate and assemble
6. **Test procedure** — how to verify the module works before installing
7. **Known limitations** — honest list of what does not work or is not tested
8. **License** — must be CERN OHL v2

---

## Community Modules

Modules in `community/modules/` are not maintained by the core project.
They may not follow all requirements above.
Each community module must clearly state its status:

- `status: experimental` — not tested in a full build
- `status: tested` — author has built and used this module
- `status: stable` — used by multiple people, no known hardware bugs
