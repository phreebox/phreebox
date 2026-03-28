# Contributing to Phreebox

You do not need permission to contribute. You need a clear head and the willingness to read the spec first.

---

## What You Can Contribute

### Hardware Module
A new or improved physical module (display, compute board, radio, etc.).

1. Read `spec/module-interface.md` — your module must satisfy the interface spec.
2. Use KiCad for schematics. No proprietary EDA tools.
3. Place your module in `community/modules/<your-module-name>/`.
4. Include: schematic, BOM, README with build instructions and test results.
5. Open a pull request. Title: `[module] Short description`.

### Software
Bug fixes, improvements to the bridge daemon, phone-os, or cube-os configs.

1. Read `software/bridge/README.md` before touching the bridge.
2. Keep changes focused. One PR = one change.
3. Include a brief explanation of *why*, not just *what*.

### Protocol Change (RFC)
Changes to `spec/` require an RFC process.

1. Copy `spec/rfcs/0000-template.md` to `spec/rfcs/XXXX-your-title.md`.
2. Fill in the template completely.
3. Open a pull request and start a discussion.
4. RFC is accepted when there is rough consensus and no unresolved objections.
5. Only then is `spec/` updated.

This process exists because **breaking the spec breaks everyone's hardware.**

### Documentation
Any improvement is welcome. Fix a typo, clarify a step, add a translation.
No RFC required. Open a PR directly.

### Porting to New Hardware
New device? Follow `docs/porting-guide.md`.
Add your port to `community/builds/<device-name>/`.

---

## The One Rule

**What you contribute must remain as free as what you received.**

Hardware contributions: CERN OHL v2.
Software contributions: GPL v3.
Documentation: CC-BY-SA 4.0.

No exceptions.

---

## Code Style

- C for the bridge daemon. POSIX only. No platform-specific APIs without abstraction.
- Shell scripts: POSIX sh, not bash-specific syntax.
- Markdown: no trailing whitespace. Blank line between sections.
- Commit messages: imperative mood. `Add display module spec`, not `Added` or `Adding`.

---

## Questions

Open an issue. Label it `question`.
There are no stupid questions about hardware you're trying to build.
