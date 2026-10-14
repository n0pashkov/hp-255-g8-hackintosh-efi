# HP 255 G8 Hackintosh — OpenCore for macOS Ventura

English | [Русский](README.ru.md)

This repository contains a machine-specific OpenCore EFI for the **HP 255 G8** with an AMD Ryzen 5 5500U. The published configuration uses OpenCore 1.0.7 and was verified with macOS Ventura 13.7.8 (22H730). It is not a universal laptop EFI.

## Feature status

| Feature | Status | Notes |
|---|---|---|
| Boot macOS Ventura 13.7.8 (22H730) | Working | Verified on this laptop; this is the published profile. |
| Renoir graphics and built-in 1920×1080 display | Working | Verified with the published EFI. |
| Samsung NVMe storage | Working | macOS Ventura was captured running from the internal SSD. |
| Intel AX200 Wi-Fi on Ventura | Working | `AirportItlwm` 2.3.0 loaded; Wi-Fi was connected on `en1` during the live check. A previous test reached 867 Mbps. |
| Realtek Ethernet | Working | User reports normal operation; `RealtekRTL8111` 3.0.4 loaded. `en0` had no active link during the live check. |
| Built-in speakers and microphone | Working | `AppleALC` 1.9.7 with `alcid=3`. |
| Brightness slider and function keys | Working | Published ACPI setup and `BrightnessKeys` 1.0.3. |
| I2C touchpad and buttons | Working | `VoodooI2C` 2.8 and `VoodooI2CHID`. |
| macOS Sequoia 15 boot | Partially working | Booted in an experiment; the published EFI is not validated for Sequoia. |
| Intel AX200 Wi-Fi on Sequoia | Not working | `AirportItlwm` stayed unloaded and Wi-Fi was unavailable in the recorded test. |
| Touchpad with VoodooI2C 2.9.1 | Not working | Test logged `VoodooI2CHIDDevice start failed`; the published profile uses 2.8. |
| Battery reporting | Partially working | macOS reported 100% charged on AC, Condition Normal, and 0 cycles; discharge accuracy was not tested. |
| Intel Bluetooth | Not tested | System Profiler reported the controller Off; `IntelBluetoothFirmware` was not in the loaded-kext list. |
| Camera, HDMI, sleep/wake, and USB ports | Not tested | No end-to-end test was recorded; a validated custom USB map is not documented. |
| Other macOS releases | Not tested | No results were recorded for other versions. |

The live read-only snapshot was collected on 2026-10-15. It did not include SSIDs, MAC addresses, or serial numbers.

The Sequoia-specific kext entries in `config.plist` are disabled. The file also contains a few AMD kernel patches scoped to Darwin 24.0.0–25.99.99; those entries do not make the complete EFI a validated Sequoia or later profile. AMD patches, kexts, and kernel limits must be checked together for the target release. See the [Dortania AMD guide](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html#kernel).

## Hardware

See [hardware details](docs/hardware-info.md). The tested setup has a Ryzen 5 5500U, 16 GB DDR4, Radeon Renoir graphics, Samsung 256 GB NVMe storage, an Intel AX200 Wi-Fi card, Realtek Ethernet, and a Full HD panel.

The factory Realtek RTL8852AE Wi-Fi card was replaced with an Intel AX200NGW. The RTL8852AE worked in Linux during the setup, but a suitable macOS driver was not identified at that time.

## Before using this EFI

1. Back up the EFI currently used to boot the laptop.
2. Generate your own SMBIOS values with GenSMBIOS and set them under `PlatformInfo -> Generic`. The values in this repository are placeholders.
3. Use the Ventura `AirportItlwm.kext` entry for this profile. Do not enable `AirportItlwm_Sequoia.kext` or combine `AirportItlwm` with `itlwm`.
4. Validate the edited configuration with the `ocvalidate` version matching OpenCore 1.0.7.
5. Test boot, Wi-Fi, sound, brightness, and the touchpad from a backup boot device before replacing your working EFI.

After changing SMBIOS or NVRAM settings, use **Reset NVRAM** from the OpenCore picker and check that macOS still boots.

`itlwm.kext` is intentionally absent. An older local copy contained saved Wi-Fi profiles, so it was removed before publication. Do not add private profile data to shared kexts.

## Repository contents

- `EFI/BOOT` — UEFI boot files.
- `EFI/OC/ACPI` — ACPI tables for this laptop, including EC/USBX, HPET, CPU power management, RTC, display brightness, and XOSI.
- `EFI/OC/Kexts` — kexts referenced by `config.plist`.
- `EFI/OC/Drivers` and `EFI/OC/Tools` — OpenCore drivers and tools.
- `EFI/OC/Resources` — OpenCore picker resources.
- [Kext versions and status](docs/kexts.md).
- [Troubleshooting and recovery](docs/troubleshooting.md).
- [Change log](CHANGELOG.md).

The repository does not include macOS Recovery, logs, NVRAM dumps, real serial numbers, UUIDs, MAC addresses, saved network profiles, or old backup `config.plist` files. Third-party kexts retain their own licenses and attribution.
