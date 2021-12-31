# Prometheus ESP8266 DHT Exporter

[![GitHub release](https://img.shields.io/github/v/release/HON95/prometheus-esp8266-dht-exporter?label=Version)](https://github.com/HON95/prometheus-esp8266-dht-exporter/releases)

An IoT Prometheus exporter for measuring temperature and humidity, using an ESP8266 (Arduino-compatible) with a Wi-Fi module and a DHT (temperature + humidity) sensor.

## Metrics

| Metric | Description | Unit |
| - | - | - |
| `iot_up` | Metadata about the device. | |
| `iot_air_humidity_percent` | Air humidity. | `%` |
| `iot_air_temperature_celsius` | Air temperature. | `°C` |
| `iot_air_heat_index_celsius` | Apparent air temperature, based on temperature and humidity. | `°C` |

## Requirements

### Hardware

- ESP8266-based board (or some other appropriate Arduino-based board).
    - Tested with "Adafruit Feather HUZZAH ESP8266" and "WEMOS D1 Mini".
- DHT sensor.
    - Tested with a cheap DHT11 from eBay and "Wemos DHT Shield" (using pin 2).
    - DHT11 supports a maximum of 1Hz polling while DHT22 supports a maximum of 2Hz polling.
    - Both DHT11 and DHT22 support both 3V and 5V at 2.5mA max current.

### Software

- [Arduino IDE](https://www.arduino.cc/en/Main/Software)
    - Download and install.
- [esp8266 library for Arduino](https://github.com/esp8266/Arduino#installing-with-boards-manager)
    - See the instructions on the page.
- [DHT sensor library](https://github.com/adafruit/DHT-sensor-library)
    - Install using the Arduino library manager.

## Building

### Hardware

Using the "Adafruit Feather HUZZAH ESP8266".

Wire the DHT sensor power to the 3.3V and any GND on the ESP and wire the data output to e.g. pin 14 (aka D5).

### Software

Using PlatformIO (VSCode).

Must build with CLI tools, create .env file and source it
```sh
export WIFI_SSID='\"<SSID>\"'
export WIFI_PASSWORD='\"<PASS>\"'
```

On Windows create `.env.ps1`
```ps
$env:WIFI_SSID='\"<SSID>\"'
$env:WIFI_PASSWORD='\"<PASS>\"'
```

The escaped quotes are important!

Build

```sh
source .env
# On windows use 
. .env.ps1
pio run -e dht01
```

Upload (also builds)

```sh
pio run -e dht01 -t upload
```

## Version

See `src/version.h`.

It's set manually since no build tools (or CI) other than the Arduino IDE is used.

## License

GNU General Public License version 3 (GPLv3).
