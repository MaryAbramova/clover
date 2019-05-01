# Модуль ESP8266

> **Note** Более подробную информацию можно найти в [основной статье](https://docs.px4.io/en/telemetry/esp8266_wifi_module.html) в официальной документации и в [репозитории с прошивкой](https://github.com/dogmaphobic/mavesp8266) для ESP8266.

![ESP8266 on top of Pixracer](../assets/esp8266_pixracer_top_wifi.jpg)

Полётные контроллеры семейства Pixracer поддерживают подключение Wi-Fi модулей ESP8266. Эти модули можно использовать для подключения к полётному контроллеру с компьютера или планшета, даже если бортовой компьютер (например, [Raspberry Pi](raspberry.md)) отсутствует или неисправен.

> **Hint** Для Клевера предпочтительнее связываться с полётным контроллером [через Raspberry Pi](gcs_bridge.md).

## Подготовка модуля

Перед началом работы в модуль ESP8266 следует загрузить прошивку с поддержкой MAVLink. Для этого потребуется:

* [сама прошивка](http://www.grubba.com/mavesp8266/firmware-1.2.2.bin);
* компьютер с ОС на базе GNU/Linux;
* USB-UART адаптер;
* утилита [esptool](https://github.com/espressif/esptool).

> **Warning** Убедитесь в том, что на вашем USB-UART адаптере установлено напряжение **3.3 В**!

Подключите ваш модуль к USB-UART, как показано на схеме:

![ESP8266 flashing setup](../assets/esp8266_flashing_ftdi.jpg)

Скачайте [прошивку для модуля](http://www.grubba.com/mavesp8266/firmware-1.2.2.bin). Подключите USB-UART к компьютеру и посмотрите, какое устройство соответствует переходнику. Убедитесь, что у вас установлена утилита esptool (её можно поставить командой `pip install esptool`). Запустите процесс загрузки прошивки командой:

```bash
esptool.py --baud 921600 --port /dev/ttyUSB0 write_flash 0x00000 firmware-1.2.2.bin
```

Вместо `/dev/ttyUSB0` укажите устройство, соответствующее вашему переходнику, а вместо `firmware-1.2.2.bin` - путь к прошивке.

> **Hint** Если в процессе загрузки прошивки возникли проблемы, вы можете запустить процесс заново.

## Работа с ESP8266

![ESP8266 connection scheme](../assets/esp8266_pixracer_connection.jpg)

Подключите ESP8266 к Pixracer так, как показано на схеме, и включите полётный контроллер. В списке доступных Wi-Fi сетей появится сеть `PixRacer` с паролем по умолчанию `pixracer`. Подключитесь к этой сети и запустите QGroundControl. Программа должна автоматически установить соединение с полётным контроллером.

> **Info** Если автоматическое подключение не происходит, проверьте, что в настройках QGroundControl включено автоматическое подключение по UDP.

![QGroundControl connection via ESP8266](../assets/esp8266_qgroundcontrol.png)

В меню настроек полётного контроллера появится вкладка **WiFi Bridge**. В ней можно изменить некоторые параметры модуля, например, режим работы (точка доступа/клиент), название и пароль Wi-Fi сети.

![QGroundControl ESP8266 settings pane](../assets/esp8266_qgroundcontrol_settings.png)

> **Warning** Настоятельно рекомендуется поменять стандартные параметры сети!

Также эти параметры можно поменять в веб-интерфейсе модуля, доступном по умолчанию по адресу [http://192.168.4.1/setup](http://192.168.4.1/setup).

![ESP8266 native Web interface](../assets/esp8266_web_interface.png)