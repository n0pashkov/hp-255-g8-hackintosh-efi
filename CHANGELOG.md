# Changelog

English | [Русский](CHANGELOG.ru.md)

## 2026-10-15

- Replaced the README feature list with a four-state table: working, partially working, not working, and not tested.
- Added English originals and linked Russian translations for the README and hardware, kext, troubleshooting, and change log documents.
- Recorded the actual support boundary: Ventura 13.7.8 is verified; Sequoia booted experimentally, but AX200 Wi-Fi did not work and the published EFI is not a Sequoia profile.
- Added setup findings for the AX200 replacement, VoodooI2C version choice, audio, and brightness ACPI.
- Clarified which functions have no recorded test and added the enabled `AppleMCEReporterDisabler` entry to the kext inventory.

## 2026-10-14

- Captured the working EFI from the HP 255 G8 internal SSD running macOS Ventura 13.7.8.
- Recorded AirportItlwm 2.3.0, AppleALC 1.9.7, BrightnessKeys 1.0.3, and VoodooI2C 2.8.
- Removed old backup configurations and `.previous` kext copies.
- Replaced SMBIOS and unique identifiers with placeholder values.
