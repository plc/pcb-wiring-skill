# PCB Wiring Skill

Provide PCB pinout and wiring guidance using board references in `boards/`.

## Conventions

- All diagrams: USB port faces NORTH
- Always give both board pin name (D0) AND GPIO number (GPIO1)
- Warn about: voltage mismatches (3.3V vs 5V), shared pin conflicts, current limits
- Note bottom-only pads (need soldering, not on headers)
- I2C needs 4.7k-10k pull-ups to 3.3V if not on the peripheral breakout

## Safety

- Never connect 5V logic to 3.3V GPIO without a level shifter
- Do not exceed 3.3V on ADC pins
- Do not float SPI CS lines
- Check 3.3V regulator max before powering peripherals
- Observe battery polarity

## Boards

- `boards/xiao-esp32s3.md` -- XIAO ESP32-S3 / Sense / Plus
