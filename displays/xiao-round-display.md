# Seeed Studio Round Display for XIAO

Source: https://wiki.seeedstudio.com/get_start_round_display/

1.28" 240x240 round TFT with capacitive touch. GC9A01 display driver, CHSC6X touch controller, PCF8563 RTC. SPI display + I2C touch/RTC. 3.7V LiPo charging via JST 1.25. MicroSD slot. Plugs directly onto XIAO header (socket connector, no separate pin header).

## XIAO Interface Mapping

The board mates directly onto the XIAO socket. All 14 header pins are used.

```
                  +---XIAO socket---+
                  |                 |
  BAT_ADC    D0 -|o               o|- 5V
  LCD_CS     D1 -|o               o|- GND
  SD_CS      D2 -|o               o|- 3V3
  LCD_DC     D3 -|o  Round Disp  o|- D10  SD_MOSI / LCD_MOSI
  I2C_SDA    D4 -|o  (back side) o|- D9   SD_MISO / LCD_MISO
  I2C_SCL    D5 -|o               o|- D8   SD_SCK  / LCD_SCK
  LCD_BL     D6 -|o               o|- D7   TP_INT
                  +-----------------+
```

## Pin Description

- D0 (A0) -- Battery voltage ADC. On v1.1, selectable via DIP switch (position 1)
- D1 -- LCD chip select, active low (GC9A01 CS)
- D2 -- SD card chip select, active low (microSD CS)
- D3 -- LCD data/command select (GC9A01 DC)
- D4 (SDA) -- I2C data, shared by touch controller (CHSC6X) and RTC (PCF8563)
- D5 (SCL) -- I2C clock, shared by touch controller (CHSC6X) and RTC (PCF8563)
- D6 -- LCD backlight (PWM capable). On v1.1, selectable via DIP switch (position 2)
- D7 -- Touch interrupt (active low)
- D8 (SCK) -- SPI clock, shared by display and SD card
- D9 (MISO) -- SPI MISO, shared by display and SD card
- D10 (MOSI) -- SPI MOSI, shared by display and SD card
- 5V -- 5V power input
- GND -- Ground
- 3V3 -- 3.3V power input

## SPI Bus (shared)

Display (GC9A01) and microSD share the SPI bus on D8/D9/D10. Use chip select lines (D1 for display, D2 for SD) to select the active device. Do not access both simultaneously.

## I2C Bus (shared)

Touch controller and RTC share the I2C bus on D4/D5.

- CHSC6X touch controller -- address 0x2E
- PCF8563 RTC -- address 0x51

## Onboard Components

- **Display:** 1.28" 240x240 IPS TFT, GC9A01 driver, SPI
- **Touch:** CHSC6X capacitive touch, I2C
- **RTC:** PCF8563, I2C, CR927 backup battery (positive terminal facing out)
- **SD card:** MicroSD slot, FAT32, max 32GB
- **Battery:** JST 1.25 connector, 3.7V LiPo, onboard charge IC
- **PMIC:** ETA3410
- **Power switch:** Physical slide switch

## v1.0 vs v1.1 Differences

- v1.1 adds a 2-position DIP switch to free D0 (A0) and D6 for general GPIO use
  - Switch position 1: connects/disconnects D0 from battery voltage divider
  - Switch position 2: connects/disconnects D6 from backlight circuit
- v1.1 changes the Li battery charge IC
- v1.1 labels the SD slot as "MicroSD Slot" (was "TF Slot" on v1.0)
