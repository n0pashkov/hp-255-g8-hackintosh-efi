# Troubleshooting and recovery

English | [Русский](troubleshooting.ru.md)

This EFI is a Ventura profile for one HP 255 G8 hardware setup. Back up the working EFI before changing kexts, ACPI tables, or SMBIOS values.

## Check the active setup

- In the OpenCore picker, choose **Reset NVRAM** after changing SMBIOS or NVRAM settings.
- In macOS, inspect loaded extensions with `kmutil showloaded` and confirm that the expected kexts are present.
- Check the [kext inventory](kexts.md) for the enabled Ventura entries and their kernel ranges.
- The repository does not document a validated custom USB map. Do not assume every port, camera, HDMI, Bluetooth, or sleep/wake has been tested.

## Wi-Fi is missing

1. Confirm the OS is Ventura 13.7.x and that `AirportItlwm.kext` 2.3.0 is enabled. In this configuration it is limited to kernel versions 22.0–22.99.99.
2. Confirm `itlwm.kext` is not loaded alongside `AirportItlwm`. `itlwm.kext` is not included in this repository.
3. Recheck the matching `Kernel -> Add` entry and bundle path in `config.plist`; reset NVRAM after configuration changes.
4. Do not use this Ventura profile as Sequoia Wi-Fi support. In the recorded Sequoia experiment, the OS booted and the OCLP-Mod root patch completed, but `AirportItlwm` stayed unloaded and AX200 Wi-Fi did not work.

## Touchpad does not start

The published profile uses `VoodooI2C` 2.8 and `VoodooI2CHID`. In testing, `VoodooI2C` 2.9.1 logged `VoodooI2CHIDDevice start failed` and did not expose the pointing device. If updating caused this failure, restore the 2.8 kext set and check that all VoodooI2C bundle paths and order match `config.plist`.

The tested touchpad was ACPI device `ELAN072B` on controller `AMDI0010`. Another laptop revision may expose different ACPI devices.

## Brightness control is missing

This EFI uses `SSDT-PNLF.aml`, `SSDT-GP17ALIS.aml`, `SSDT-XOSI.aml`, and `BrightnessKeys` 1.0.3. During setup, a PNLF device nested under `GP17.VGA` left the brightness slider unavailable; the working arrangement exposed PNLF at the ACPI root with UID 19. These ACPI changes are specific to this machine, so compare against its published files instead of copying them to another model blindly.

## Audio is missing

The tested audio setup is `AppleALC` 1.9.7 with boot argument `alcid=3`. Check the boot argument and confirm that AppleALC is enabled and loaded. The built-in speakers and microphone were confirmed with this combination.

## Restore a bootable EFI

1. Keep a copy of the EFI currently used to boot the laptop.
2. Restore the repository EFI from a separate boot device and test it before replacing the working copy.
3. Generate your own SMBIOS values before using the configuration on another installation.
4. Keep the backup boot device until Wi-Fi, audio, brightness, and the touchpad work on your own machine.
