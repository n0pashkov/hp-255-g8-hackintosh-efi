# HP 255 G8 Hackintosh — OpenCore Ventura

Рабочая конфигурация OpenCore для **HP 255 G8** с AMD Ryzen 5 5500U. Она собрана на OpenCore 1.0.7 и проверена на macOS Ventura 13.7.8. В репозитории сохранены EFI, ACPI, драйверы и кексты, необходимые для этой конкретной машины.

> Конфигурация не универсальная. Перед использованием нужно сгенерировать собственные SMBIOS-значения и проверить настройки BIOS.

## Что работает

- загрузка macOS Ventura через OpenCore;
- встроенная AMD Renoir-графика через `NootedRed`;
- внутренний дисплей 1920×1080;
- Intel AX200: системный Wi‑Fi через `AirportItlwm`;
- внутренние динамики и микрофон через `AppleALC` (`alcid=3`);
- аппаратные клавиши яркости через `BrightnessKeys`;
- тачпад/кнопки через `VoodooI2C 2.8` и `VoodooI2CHID`;
- NVMe через `NVMeFix`;
- батарея через `SMCBatteryManager`;
- Realtek Ethernet через `RealtekRTL8111`;
- Bluetooth-кексты Intel включены в конфигурацию.

## Аппаратная конфигурация

Полная таблица находится в [`docs/hardware-info.md`](docs/hardware-info.md). Кратко: Ryzen 5 5500U (6 ядер/12 потоков), 16 ГБ DDR4, AMD Radeon Renoir, Samsung NVMe 256 ГБ, Intel AX200 и Full HD-панель.

## Важные правила

1. Использовать `AirportItlwm.kext` для Ventura. `itlwm.kext` удалён из опубликованной EFI; одновременно загружать оба варианта нельзя.
2. `AirportItlwm_Sequoia.kext`, `AMFIPass.kext`, `IOSkywalkFamily.kext` и `IO80211FamilyLegacy.kext` отключены в текущем Ventura-профиле.
3. Значения `SystemSerialNumber`, `MLB`, `SystemUUID` и `ROM` в опубликованном `config.plist` заменены безопасными заглушками. Перед использованием сгенерируйте свои значения через GenSMBIOS.
4. После изменения NVRAM или SMBIOS выполните Reset NVRAM из меню OpenCore и проверьте загрузку.
5. Не копируйте этот EFI на другой ноутбук без отдельной настройки ACPI, DeviceProperties и USB.

## Установка

1. Скачайте репозиторий и скопируйте каталог `EFI` на EFI-раздел загрузочного диска.
2. Откройте `EFI/OC/config.plist` в ProperTree.
3. Замените SMBIOS-значения в `PlatformInfo -> Generic`.
4. Проверьте, что для Ventura включён только `AirportItlwm.kext`.
5. Проверьте конфигурацию через `ocvalidate`, затем загрузитесь и выполните Reset NVRAM.
6. Проверьте Wi‑Fi, звук, яркость и тачпад до удаления резервного загрузчика.

## Состав

- `EFI/BOOT` — стандартный UEFI-загрузчик;
- `EFI/OC/ACPI` — SSDT для EC/USBX, HPET, питания CPU, RTC, панели и XOSI;
- `EFI/OC/Kexts` — кексты, перечисленные в `config.plist`;
- `EFI/OC/Drivers` и `EFI/OC/Tools` — OpenRuntime, HfsPlus, ResetNvramEntry и OpenShell;
- `EFI/OC/Resources` — ресурсы меню OpenCore;
- [`docs/kexts.md`](docs/kexts.md) — версии и назначение кекстов;
- [`docs/troubleshooting.md`](docs/troubleshooting.md) — восстановление и диагностика.

## Ограничения

В репозиторий намеренно не включены Recovery, логи, дампы NVRAM, серийные номера, UUID, MAC-адреса, сетевые настройки и старые резервные `config.plist`. Сторонние кексты сохраняют собственные лицензии и авторство.
