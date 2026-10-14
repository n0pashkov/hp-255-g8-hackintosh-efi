# Hardware configuration

English | [Русский](hardware-info.ru.md)

This inventory describes the laptop tested with macOS Ventura 13.7.8. Unique machine identifiers are omitted.

| Component | Value |
|---|---|
| Laptop | HP 255 G8 |
| CPU | AMD Ryzen 5 5500U with Radeon Graphics, 6 cores / 12 threads; reported by `sysctl` |
| Memory | 16 GB DDR4, 2 × 8 GB; System Profiler reports 2667 MHz and status OK for both modules |
| GPU | AMD Radeon RX Renoir Graphics, PCI ID `1002:164c`, HP subsystem `103c`; Metal 3; macOS reports 512 MB VRAM |
| Display | Built-in Full HD, 1920 × 1080, 60 Hz; reported as main and online |
| SSD | Samsung MZVL4256HBJD-00BH1 NVMe, 256.06 GB, firmware `HPS3NHAV`, PCIe x4 at 8.0 GT/s; SMART verified |
| Wi-Fi | Intel AX200, PCI ID `8086:2723`, interface `en1`, `AirportItlwm` 2.3.0 |
| Ethernet | Realtek, interface `en0`, `RealtekRTL8111.kext` 3.0.4 |
| Audio | Built-in speakers and microphone; 2 channels each; AppleALC layout `3` |
| Battery | System Profiler reported Condition Normal and 0 cycles; at capture it showed 100% charged on AC |
| Bluetooth | System Profiler reported a USB controller `BCM_4350C2`, state Off; Bluetooth functionality was not confirmed |
| Touchpad | I2C HID, VoodooI2C 2.8 and VoodooI2CHID |
| SMBIOS | MacBookPro16,3 |
| Operating system | macOS Ventura 13.7.8 (22H730), Darwin kernel 22.6.0 |
| OpenCore | 1.0.7 |

## Recorded checks

- The AX200 connected through the macOS AirPort interface. Link speed reached 867 Mbps during one test; actual speed depends on the access point and network.
- In the live SSH capture on 2026-10-15, Wi-Fi interface `en1` was active and associated. The network name was omitted. The user reports that Wi-Fi works correctly.
- The user reports that Realtek Ethernet worked without problems. `RealtekRTL8111` 3.0.4 was loaded; interface `en0` showed no active link during the SSH capture.
- AppleALC exposed the built-in audio input and output. Speakers and microphone were confirmed with layout `3`.
- The live system reported the internal NVMe as SMART verified, 256.06 GB, PCIe x4 at 8.0 GT/s.
- The battery was reported as 100% charged on AC, Condition Normal, and 0 cycles. Charge and health values were not independently checked during discharge.
- The Bluetooth controller was reported Off. `IntelBTPatcher` 2.3.0 and `BlueToolFixup` 2.7.2 were loaded; `IntelBluetoothFirmware` did not appear in the loaded-kext listing. Bluetooth operation remains unverified.
- Brightness control worked with the published ACPI tables and `BrightnessKeys` 1.0.3.
- VoodooI2C 2.8 is the version retained in the published configuration. VoodooI2C 2.9.1 failed to start the HID device on this setup (`VoodooI2CHIDDevice start failed`).

The live snapshot was collected from macOS on 2026-10-15. System Profiler identifies the SMBIOS as `MacBookPro16,3`; `sysctl` reports the physical CPU model as AMD Ryzen 5 5500U. SMBIOS fields identify the macOS model and are not the laptop's physical HP model or BIOS revision. The reported 512 MB graphics memory is an iGPU value, not dedicated VRAM.

## Hardware changes and identification

The factory Realtek RTL8852AE Wi-Fi adapter (`10ec:8852`) was replaced with an Intel AX200NGW (HP SPS L35282-005). The Realtek card worked in Linux during the setup, but no suitable macOS driver was identified then. A separate Intel 3165 trial did not expose its Wi-Fi PCI device in this laptop; its Bluetooth USB function was visible. These observations apply to the tested machine and are not a general compatibility verdict for those adapters.

The touchpad appears as ACPI device `ELAN072B` (`PNP0C50`) on the AMD I2C controller `AMDI0010`, address `0x15`, in polling mode. These identifiers can help when comparing another unit, but do not guarantee that its ACPI tables match.

The SMBIOS product name and all unique identifiers, including serial number, MLB, UUID, ROM, MAC addresses, and network addresses, are intentionally not published here.
