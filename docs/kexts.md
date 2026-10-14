# Кексты

Список соответствует опубликованному `config.plist`. Статус `активен` означает, что запись включена для текущей Ventura-конфигурации.

| Кекст | Версия | Статус | Назначение |
|---|---:|---|---|
| Lilu | 1.7.2 | активен | Платформа патчей |
| VirtualSMC | 1.3.7 | активен | SMC и датчики |
| NootedRed | 0.8.10 | активен | AMD Renoir-графика |
| AppleALC | 1.9.7 | активен | Звук, layout 3 |
| NVMeFix | 1.1.3 | активен | Совместимость NVMe |
| RealtekRTL8111 | 3.0.4 | активен | Проводная сеть |
| VoodooPS2Controller | 2.3.7 | активен | Клавиатура PS/2 |
| VoodooI2C | 2.8 | активен | I2C-контроллер тачпада |
| VoodooI2CHID | 1.0 | активен | HID-тачпад |
| SMCBatteryManager | 1.3.7 | активен | Батарея |
| BrightnessKeys | 1.0.3 | активен | Fn-клавиши яркости |
| IntelBluetoothFirmware | 2.3.0 | активен | Прошивка Bluetooth |
| IntelBTPatcher | 2.3.0 | активен | Bluetooth-патчи |
| BlueToolFixup | 2.7.2 | активен | Bluetooth в новых macOS |
| AirportItlwm | 2.3.0 | активен | Нативный Wi‑Fi в Ventura |
| USBToolBox | 1.2.0 | отключён | USB-карта, оставлена для совместимости |
| UTBDefault | 1.0 | отключён | USB-инжектор |
| IOSkywalkFamily | 1.0 | отключён | Sequoia-патч |
| IO80211FamilyLegacy | 12.0 | отключён | Sequoia-патч |
| AMFIPass | 1.4.1 | отключён | Sequoia/OCLP-патч |
| AirportItlwm_Sequoia | 2.4.0 | отключён | Вариант для Sequoia |

`itlwm` намеренно не включён в репозиторий: он конфликтует с системным вариантом и в старой копии содержал сохранённые Wi‑Fi-профили. Для Ventura используется `AirportItlwm`, который появляется как обычный системный Wi‑Fi интерфейс.
