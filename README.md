# Waveshare ESP32-S3 Audio Board - ESPHome Configuration

ESPHome configuration for the [Waveshare ESP32-S3 Audio Board](https://www.waveshare.com/esp32-s3-audio-board.htm) as a Home Assistant voice assistant with wake word detection.

## Hardware

- **Board**: [Waveshare ESP32-S3-AUDIO-Board](https://www.waveshare.com/wiki/ESP32-S3-AUDIO-Board)
- **MCU**: ESP32-S3 (16MB Flash, 8MB Octal PSRAM)
- **Audio ADC**: ES7210 (quad-channel, used for microphone input)
- **Audio DAC**: ES8311 (mono codec, used for speaker output)
- **I/O Expander**: TCA9555 (buttons, speaker amp enable)
- **RTC**: PCF85063
- **LEDs**: 7x WS2812 RGB ring (GPIO38)
- **Buttons**: 3 keys via TCA9555 (Vol Down, Assist, Vol Up)

## Features

- Wake word detection ("Okay Nabu") running on-device via `micro_wake_word`
- Voice assistant pipeline with Home Assistant
- LED ring animations for each voice assistant state (listening, thinking, speaking, etc.)
- Physical buttons for volume control and manual assist trigger
- Media player support

## Pin Mapping

See [`pinout.yaml`](pinout.yaml) and [`pinout.json`](pinout.json) for machine-readable pin assignments.

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

### I2C Devices

| Device | Address | Function |
|--------|---------|----------|
| TCA9555 | 0x20 | I/O expander (buttons, amp enable) |
| ES8311 | 0x18 | Audio DAC |
| ES7210 | 0x40 | Audio ADC |
| PCF85063 | 0x51 | Real-time clock |

## Setup

1. Copy `secrets.yaml.example` to `secrets.yaml` and fill in your values
2. Install [ESPHome](https://esphome.io/)
3. Flash: `esphome run speaker.yaml`

## Files

- `speaker.yaml` - Main ESPHome configuration
- `pinout.yaml` - Machine-readable pin mapping (YAML)
- `pinout.json` - Machine-readable pin mapping (JSON)
- `secrets.yaml.example` - Template for secrets

## License

MIT
