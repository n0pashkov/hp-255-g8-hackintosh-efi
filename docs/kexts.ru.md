# Список кекстов

[English](kexts.md) | Русский

Версии и статусы ниже взяты из самих кекстов и опубликованного `EFI/OC/config.plist`. **Включён** означает, что запись включена в Ventura-профиле; само по себе это не доказывает, что функция была проверена.

| Кекст | Версия | Статус | Назначение в этой EFI |
|---|---:|---|---|
| Lilu | 1.7.2 | Включён | Общая платформа патчей |
| VirtualSMC | 1.3.7 | Включён | Эмуляция SMC и датчики |
| AppleMCEReporterDisabler | 1.2 | Включён | Совместимость macOS с AMD; руководство AMD требует его для macOS 12.3 и новее |
| NootedRed | 0.8.10 | Включён | Поддержка графики Renoir |
| AppleALC | 1.9.7 | Включён | Звук; layout `3` |
| NVMeFix | 1.1.3 | Включён | Совместимость NVMe |
| RealtekRTL8111 | 3.0.4 | Включён | Проводная сеть Realtek |
| VoodooPS2Controller | 2.3.7 | Включён | Клавиатура PS/2; её плагин включён |
| VoodooI2C | 2.8 | Включён | I2C-контроллер и поддержка устройств ввода |
| VoodooI2CHID | 1 | Включён | I2C HID-тачпад |
| SMCBatteryManager | 1.3.7 | Включён | Отображение батареи |
| BrightnessKeys | 1.0.3 | Включён | Функциональные клавиши яркости |
| IntelBluetoothFirmware | 2.3.0 | Включён | Прошивка Intel Bluetooth |
| IntelBTPatcher | 2.3.0 | Включён | Поддержка Intel Bluetooth |
| BlueToolFixup | 2.7.2 | Включён | Поддержка Bluetooth в новых macOS |
| AirportItlwm | 2.3.0 | Включён | Wi‑Fi Intel для Ventura; диапазон ядра 22.0–22.99.99 |
| USBToolBox | 1.2.0 | Отключён | Инструмент настройки USB-карты |
| UTBDefault | 1.0 | Отключён | Стандартная карта USBToolBox |
| IOSkywalkFamily | 1.0 | Отключён | Сетевой компонент для Sequoia |
| IO80211FamilyLegacy | 1200.12.2b1 | Отключён | Сетевой компонент для Sequoia |
| AMFIPass | 1.4.1 | Отключён | Экспериментальный компонент Sequoia/OCLP |
| AirportItlwm_Sequoia | 2.4.0 | Отключён | Сборка Wi‑Fi Intel для Sequoia |

Записи для Sequoia присутствуют, но отключены. В эксперименте Sequoia загрузилась, однако `AirportItlwm` не загрузился и AX200 осталась без Wi‑Fi. Этот список кекстов не является профилем с поддержкой Sequoia. В `config.plist` также есть несколько AMD kernel patches с диапазоном Darwin 24.0.0–25.99.99; их наличие не подтверждает работу всей EFI на этих системах. `USBToolBox` и `UTBDefault` отключены; проверенная собственная USB-карта в репозитории не описана.

`itlwm.kext` не включён в репозиторий. Его удалили до публикации, потому что в старой локальной копии были сохранённые профили Wi‑Fi. В этой Ventura-EFI используйте только включённую запись `AirportItlwm.kext`.

Требование к `AppleMCEReporterDisabler` для версий macOS с AMD описано в [руководстве Dortania по AMD](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html#kernel). Приведённые версии относятся к текущему снимку репозитория и не означают, что каждый кекст нужно обновлять независимо.
