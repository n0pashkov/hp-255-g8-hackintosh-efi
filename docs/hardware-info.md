# Hardware configuration

English | [Русский](hardware-info.ru.md)

This inventory describes the laptop tested with macOS Ventura 13.7.8. Unique machine identifiers are omitted.

| Component | Value |
|---|---|
| Laptop | HP 255 G8 |
| CPU | AMD Ryzen 5 5500U, 6 cores / 12 threads, 2.1 GHz base clock |
| Memory | 16 GB DDR4-2666, 2 × 8 GB |
| GPU | AMD Radeon Renoir, PCI ID `1002:164c`, HP subsystem `103c` |
| Display | Built-in Full HD, 1920 × 1080, 60 Hz |
| SSD | Samsung MZVL4256HBJD-00BH1, NVMe, about 256 GB |
| Wi-Fi | Intel AX200, PCI ID `8086:2723`, `AirportItlwm` 2.3.0 |
| Ethernet | Realtek, `RealtekRTL8111.kext` 3.0.4 |
| Audio | Built-in speakers and microphone, AppleALC layout `3` |
| Touchpad | I2C HID, VoodooI2C 2.8 and VoodooI2CHID |
| SMBIOS | MacBookPro16,3 |
| Operating system | macOS Ventura 13.7.8 (22H730) |
| OpenCore | 1.0.7 |

## Recorded checks

- The AX200 connected through the macOS AirPort interface. Link speed reached 867 Mbps during one test; actual speed depends on the access point and network.
- AppleALC exposed the built-in audio input and output. Speakers and microphone were confirmed with layout `3`.
- Brightness control worked with the published ACPI tables and `BrightnessKeys` 1.0.3.
- VoodooI2C 2.8 is the version retained in the published configuration. VoodooI2C 2.9.1 failed to start the HID device on this setup (`VoodooI2CHIDDevice start failed`).

## Hardware changes and identification

The factory Realtek RTL8852AE Wi-Fi adapter (`10ec:8852`) was replaced with an Intel AX200NGW (HP SPS L35282-005). The Realtek card worked in Linux during the setup, but no suitable macOS driver was identified then. A separate Intel 3165 trial did not expose its Wi-Fi PCI device in this laptop; its Bluetooth USB function was visible. These observations apply to the tested machine and are not a general compatibility verdict for those adapters.

The touchpad appears as ACPI device `ELAN072B` (`PNP0C50`) on the AMD I2C controller `AMDI0010`, address `0x15`, in polling mode. These identifiers can help when comparing another unit, but do not guarantee that its ACPI tables match.

The SMBIOS product name and all unique identifiers, including serial number, MLB, UUID, ROM, MAC addresses, and network addresses, are intentionally not published here.
