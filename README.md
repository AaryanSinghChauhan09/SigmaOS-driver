# SigmaOS Driver

Rust library grouping device-driver interfaces and implementations for SigmaOS.
The current module tree covers PCI enumeration, AHCI, NVMe, USB, networking,
Wi-Fi, graphics, HID input, compatibility layers, and simulated devices.

## Hardware support limits

This repository contains both simulated and hardware-oriented code. A module or
driver type does not by itself establish working hardware support. Check each
driver's implementation and current CI evidence before relying on it; physical
DMA, interrupt delivery, device reset, and recovery paths require target
hardware or an explicitly scoped emulator. Avoid reporting a device as
supported based only on compilation.

## Driver contract

Before integrating a driver, document its supported device IDs and revisions,
resource ownership, DMA address and lifetime rules, interrupt model, privilege
requirements, concurrency assumptions, and failure cleanup. Keep probing and
device mechanics separate from product policy.

## Development

The crate depends on `SigmaOS-kernel` through a sibling path dependency. CI
resolves SigmaOS path dependencies and runs `cargo test --all-targets --locked`.
