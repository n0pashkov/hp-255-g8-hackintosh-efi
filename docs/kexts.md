# Kext inventory

English | [Русский](kexts.ru.md)

Versions and statuses below are read from the kext bundles and the published `EFI/OC/config.plist`. **Enabled** means that the entry is enabled in this Ventura profile; it does not by itself prove that a feature was tested.

| Kext | Version | Status | Role in this EFI |
|---|---:|---|---|
| Lilu | 1.7.2 | Enabled | Shared patching framework |
| VirtualSMC | 1.3.7 | Enabled | SMC emulation and sensors |
| AppleMCEReporterDisabler | 1.2 | Enabled | AMD macOS compatibility; required by the AMD guide for macOS 12.3 and newer |
| NootedRed | 0.8.10 | Enabled | Renoir graphics support |
| AppleALC | 1.9.7 | Enabled | Audio; layout `3` |
| NVMeFix | 1.1.3 | Enabled | NVMe compatibility |
| RealtekRTL8111 | 3.0.4 | Enabled | Realtek wired Ethernet |
| VoodooPS2Controller | 2.3.7 | Enabled | PS/2 keyboard; keyboard plug-in enabled |
| VoodooI2C | 2.8 | Enabled | I2C controller and input support |
| VoodooI2CHID | 1 | Enabled | I2C HID touchpad |
| SMCBatteryManager | 1.3.7 | Enabled | Battery reporting |
| BrightnessKeys | 1.0.3 | Enabled | Brightness function keys |
| IntelBluetoothFirmware | 2.3.0 | Enabled | Intel Bluetooth firmware |
| IntelBTPatcher | 2.3.0 | Enabled | Intel Bluetooth support |
| BlueToolFixup | 2.7.2 | Enabled | Bluetooth support on newer macOS |
| AirportItlwm | 2.3.0 | Enabled | Intel Wi-Fi for Ventura; kernel range 22.0 through 22.99.99 |
| USBToolBox | 1.2.0 | Disabled | USB mapping helper |
| UTBDefault | 1.0 | Disabled | Default USB map for USBToolBox |
| IOSkywalkFamily | 1.0 | Disabled | Sequoia networking component |
| IO80211FamilyLegacy | 1200.12.2b1 | Disabled | Sequoia networking component |
| AMFIPass | 1.4.1 | Disabled | Experimental Sequoia/OCLP component |
| AirportItlwm_Sequoia | 2.4.0 | Disabled | Intel Wi-Fi build for Sequoia |

The Sequoia entries are present but disabled. Sequoia booted in an experiment, but `AirportItlwm` did not load and AX200 Wi-Fi was unavailable. This kext list is not a Sequoia support profile. `config.plist` also contains a few AMD kernel patches scoped to Darwin 24.0.0–25.99.99; their presence does not establish that the full EFI works on those releases. `USBToolBox` and `UTBDefault` are disabled, and this repository does not document a validated custom USB map.

## Live kext load check

A read-only `kmutil showloaded` check on macOS Ventura 13.7.8 (2026-10-15) found these relevant kexts loaded: Lilu 1.7.2, VirtualSMC 1.3.7, NootedRed 0.8.10, AppleALC 1.9.7, NVMeFix 1.1.3, VoodooI2C 2.8, VoodooI2CHID 1, SMCBatteryManager 1.3.7, BrightnessKeys 1.0.3, IntelBTPatcher 2.3.0, BlueToolFixup 2.7.2, RealtekRTL8111 3.0.4, and AirportItlwm 2.3.0. This runtime list is separate from the Enabled/Disabled values in the EFI configuration.

`IntelBluetoothFirmware` 2.3.0 did not appear in that loaded-kext output; System Profiler reported the Bluetooth controller Off. Ventura also listed Apple system bundle IDs for `IOSkywalkFamily` and `IO80211FamilyLegacy`; those system entries do not mean that the disabled copies in this EFI were enabled.

`itlwm.kext` is not included. It was removed before publication because an older local copy contained saved Wi-Fi profiles. For this Ventura EFI, use the enabled `AirportItlwm.kext` entry only.

For the AMD macOS version requirements of `AppleMCEReporterDisabler`, see the [Dortania AMD guide](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html#kernel). The versions above describe this repository snapshot and are not recommendations to update every kext independently.
