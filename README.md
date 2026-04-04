# Waveshare ESP32-S3 Audio Board - ESPHome Configuration

ESPHome configuration for the [Waveshare ESP32-S3 Audio Board](https://www.waveshare.com/esp32-s3-audio-board.htm) as a Home Assistant voice assistant with wake word detection.

## Hardware

- **Board**: [Waveshare ESP32-S3-AUDIO-Board](https://www.waveshare.com/wiki/ESP32-S3-AUDIO-Board)
- **MCU**: ESP32-S3R8 (16MB Flash, 8MB Octal PSRAM, dual-core 240MHz)
- **Audio ADC**: ES7210 (quad-channel, used for microphone input)
- **Audio DAC**: ES8311 (mono codec, used for speaker output)
- **Speaker Amp**: NS4150B (mono Class-D)
- **I/O Expander**: TCA9555PWR (buttons, speaker amp, LCD, camera, SD card controls)
- **RTC**: PCF85063
- **LEDs**: 7x WS2812B RGB ring (GPIO38)
- **Buttons**: BOOT (GPIO0) + 3 keys via TCA9555
- **LCD**: 18-pin FPC, supports SPI and QSPI displays (1.47" to 3.5")
- **Camera**: DVP interface for OV2640/OV5640
- **SD Card**: SDMMC 1-bit mode
- **Battery**: MX1.25 connector for 3.7V lithium with charge management
- **USB**: Type-C (power, programming, data)

## Features

- Wake word detection ("Okay Nabu") running on-device via `micro_wake_word`
- Voice assistant pipeline with Home Assistant
- LED ring animations for each voice assistant state (listening, thinking, speaking, etc.)
- Physical buttons for volume control and manual assist trigger
- Media player support

## Pin Mapping

See [`pinout.yaml`](pinout.yaml) and [`pinout.json`](pinout.json) for the complete machine-readable pin mapping, including LCD, camera, SD card, and all TCA9555 I/O expander assignments.

### Key GPIO Assignments

| Function | Pin |
|----------|-----|
| I2C SCL | GPIO10 |
| I2C SDA | GPIO11 |
| I2S MCLK | GPIO12 |
| I2S BCLK | GPIO13 |
| I2S LRCLK | GPIO14 |
| I2S DIN (mic) | GPIO15 |
| I2S DOUT (speaker) | GPIO16 |
| WS2812 LED Ring | GPIO38 |
| LCD CS | GPIO3 |
| LCD SCLK | GPIO4 |
| LCD Backlight | GPIO5 |
| SD CLK | GPIO40 |
| SD CMD | GPIO42 |
| SD D0 | GPIO41 |
| Battery ADC | GPIO8 |
| USB D- | GPIO19 |
| USB D+ | GPIO20 |

### I2C Devices

| Device | Address | Function |
|--------|---------|----------|
| ES8311 | 0x18 | Audio DAC (speaker output) |
| ES7210 | 0x40 | Audio ADC (microphone input) |
| TCA9555 | 0x20 | 16-bit I/O expander |
| PCF85063 | 0x51 | Real-time clock |

### TCA9555 I/O Expander Pin Map

| Pin | Function |
|-----|----------|
| 0 (EXIO00) | LCD Reset |
| 1 (EXIO01) | Touch Panel Reset |
| 2 (EXIO02) | Touch Panel Interrupt |
| 3 (EXIO03) | SD Card CS |
| 4 (EXIO04) | Reserved |
| 5 (EXIO05) | Camera Power Down (active low) |
| 6 (EXIO06) | Camera Select (HIGH=Tx/Rx, LOW=USB) |
| 7 (EXIO07) | Camera/USB GPIO mux control |
| 8 (EXIO08) | Speaker amplifier enable (PA_CTRL) |
| 9 (EXIO09) | Key1 button (active low) |
| 10 (EXIO10) | Key2 button (active low) |
| 11 (EXIO11) | Key3 button (active low) |
| 12-15 | Expansion header |

## Setup

1. Copy `secrets.yaml.example` to `secrets.yaml` and fill in your values
2. Install [ESPHome](https://esphome.io/)
3. Flash: `esphome run speaker.yaml`

## Files

- `speaker.yaml` - ESPHome voice assistant configuration
- `pinout.yaml` - Complete machine-readable pin mapping (YAML)
- `pinout.json` - Complete machine-readable pin mapping (JSON)
- `secrets.yaml.example` - Template for secrets

## Sources

- [Waveshare Product Page](https://www.waveshare.com/esp32-s3-audio-board.htm)
- [Waveshare Wiki](https://www.waveshare.com/wiki/ESP32-S3-AUDIO-Board)
- [Official Waveshare Demo Code](https://files.waveshare.com/wiki/ESP32-S3-AUDIO-Board/ESP32-S3-AUDIO-Board-Demo.zip)

## License

MIT
