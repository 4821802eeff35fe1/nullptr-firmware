# nullptr Firmware — Codex Instructions

## Project

This repository is a custom firmware project for Flipper Zero.

The project is based on the official Flipper Devices firmware:

https://github.com/flipperdevices/flipperzero-firmware

The current development branch is:

firmware/dev

The goal is to build a deeply customized Flipper Zero firmware while
preserving hardware stability, maintainability, and the ability to merge
upstream firmware updates.

---

## Core rules

1. Never flash firmware to a physical Flipper Zero unless the user
   explicitly requests it.

2. Commands such as:

   ./fbt flash
   ./fbt flash_usb

   must never be executed automatically.

3. Building firmware with:

   ./fbt

   is allowed.

4. Never rewrite or replace large subsystems without first understanding
   their architecture.

5. Prefer minimal, isolated changes over large rewrites.

6. Preserve compatibility with the official Flipper build system.

7. Do not modify third-party libraries unless explicitly required.

8. Do not change hardware initialization, bootloader behavior,
   radio stack, power management, storage drivers, or low-level HAL
   unless the task explicitly requires it.

9. Before modifying an unfamiliar subsystem:
   - inspect its implementation;
   - inspect dependencies;
   - inspect application.fam;
   - locate related services;
   - understand lifecycle and ownership.

10. Never remove functionality merely because it appears unused.

---

## Build requirements

After meaningful code changes run:

./fbt

The firmware must compile successfully.

Do not consider a task complete while the build is broken.

When modifying an individual application, build the smallest useful
target first when practical, then validate the full firmware build.

---

## Code quality

Follow the existing Flipper Zero coding conventions.

Prefer:
- existing Furi APIs;
- existing GUI primitives;
- existing services;
- existing storage abstractions;
- existing notification APIs.

Avoid introducing new abstractions when the firmware already contains
an equivalent implementation.

Memory usage matters.

Flipper Zero is an embedded device.

Avoid:
- unnecessary heap allocations;
- large buffers;
- excessive threads;
- duplicated assets;
- unnecessary polling;
- blocking UI operations.

---

## Git policy

Do not commit automatically unless explicitly requested.

Do not push automatically unless explicitly requested.

Do not rebase or force-push automatically.

Before large modifications, report which files and subsystems will be
affected.

---

## Architecture policy

This project must remain reasonably mergeable with upstream
flipperdevices/flipperzero-firmware.

Prefer adding custom functionality in clearly identifiable locations.

Avoid scattering project-specific modifications across unrelated
official firmware files when an isolated implementation is possible.

---

## Project documentation

Important architectural decisions must eventually be documented in:

PROJECT.md
ARCHITECTURE.md
ROADMAP.md
DECISIONS.md

Do not invent project requirements that are not documented or provided
by the user.

---

## Security research functionality

Security and hardware research features must be implemented carefully
and clearly separated by subsystem.

Do not assume protocol behavior.

Inspect the existing Flipper implementation before modifying protocol,
RF, NFC, RFID, infrared, GPIO, USB, or Bluetooth functionality.

---

## Completion format

When completing a development task report:

1. What was changed.
2. Which files were changed.
3. Architectural decisions.
4. Build/test results.
5. Known limitations.
6. Recommended next step.
