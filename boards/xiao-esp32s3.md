# XIAO ESP32-S3

Source: https://wiki.seeedstudio.com/xiao_esp32s3_getting_started/

ESP32-S3R8, dual-core 240MHz, 8MB flash, 8MB PSRAM, WiFi + BLE 5.0, 21x17.8mm.
Variants: base, **Sense** (+ camera/mic/SD via B2B board), **Plus** (18 GPIOs, larger).

## Pinout (USB North, front view)

```
                         +---USB-C---+
                         | [R]   [B] |
  TOUCH1 GPIO1  A0  D0 -|o         o|- 5V
  TOUCH2 GPIO2  A1  D1 -|o         o|- GND
  TOUCH3 GPIO3  A2  D2 -|o         o|- 3V3 (700mA max)
  TOUCH4 GPIO4  A3  D3 -|o  XIAO   o|- D10 A10 MOSI GPIO9  TOUCH9
  TOUCH5 GPIO5 SDA  D4 -|o ESP32S3 o|- D9  A9  MISO GPIO8  TOUCH8
  TOUCH6 GPIO6 SCL  D5 -|o         o|- D8  A8  SCK  GPIO7  TOUCH7
         GPIO43 TX  D6 -|o         o|- D7  RX       GPIO44
                         |   [ANT]   |
                         +-o-------o-+
                         D11       D12
                         A11       A12
                       GPIO42    GPIO41
                      TOUCH12   TOUCH13
                       (left)   (right)
```

Reading direction: left-side labels read right-to-left toward the board; right-side
labels read left-to-right away from the board. Pin name (D0, D1...) is always closest
to the board edge.

- [R] = Reset button (directly on CHIP_PU/EN, active low)
- [B] = Boot button (GPIO0 -- hold during reset to enter download mode)
- [ANT] = U.FL WiFi/BT antenna connector (front, bottom-left)
- Charge LED (red) = front, top-left near USB (charging: on; charged: off)
- User LED = GPIO21 (active low, front, top-right near USB)
- All GPIO are 3.3V logic -- NOT 5V tolerant
- Max source/sink per GPIO: ~40mA

## Back-Only Pads (USB North, board flipped)

```
              +---USB-C---+
              |           |
        MTDO -|o         o|- MTDI
         GND -|o         o|- EN
        MTCK -|o         o|- MTMS
          D+ -|o         o|- BAT-
              |           o|- BAT+
              | [ThPAD]  o|- D-
              +-----------+
```

- MTDO/MTDI/MTCK/MTMS = JTAG debug interface
- EN = Chip enable (active high, internal pull-up)
- BAT+/BAT- = 3.7V LiPo direct connection (safe range: 3.0V-4.2V)
- D+/D- = USB data lines
- [ThPAD] = Thermal/ground pad (large, bottom-left)

## Pin Table

| Pin  | GPIO   | Analog | Touch   | Alt Function | Notes                         |
|------|--------|--------|---------|--------------|-------------------------------|
| D0   | GPIO1  | A0     | TOUCH1  |              |                               |
| D1   | GPIO2  | A1     | TOUCH2  |              |                               |
| D2   | GPIO3  | A2     | TOUCH3  |              | SD CS on Sense variant        |
| D3   | GPIO4  | A3     | TOUCH4  |              |                               |
| D4   | GPIO5  | A4     | TOUCH5  | I2C SDA      | Default I2C data              |
| D5   | GPIO6  | A5     | TOUCH6  | I2C SCL      | Default I2C clock             |
| D6   | GPIO43 | --     | --      | UART TX      | Serial1 TX                    |
| D7   | GPIO44 | --     | --      | UART RX      | Serial1 RX                    |
| D8   | GPIO7  | A8     | TOUCH7  | SPI SCK      | SD CLK on Sense               |
| D9   | GPIO8  | A9     | TOUCH8  | SPI MISO     | SD MISO on Sense              |
| D10  | GPIO9  | A10    | TOUCH9  | SPI MOSI     | SD MOSI on Sense              |
| D11  | GPIO42 | A11    | TOUCH12 |              | Bottom pad (left); PDM CLK on Sense  |
| D12  | GPIO41 | A12    | TOUCH13 |              | Bottom pad (right); PDM DATA on Sense |

Non-header pins (active but not on castellated pads):

| Function      | GPIO   | Notes                                       |
|---------------|--------|---------------------------------------------|
| User LED      | GPIO21 | Active low; not on any header               |
| Boot button   | GPIO0  | Directly on the board; strapping pin        |

## Bus Defaults (Arduino)

| Bus  | Pins                       | Notes                    |
|------|----------------------------|--------------------------|
| I2C  | SDA=D4, SCL=D5            | Wire library, 3.3V       |
| SPI  | SCK=D8, MISO=D9, MOSI=D10 | CS is user-defined       |
| UART | TX=D6, RX=D7              | Serial1; Serial0=USB CDC |

## Power

- USB-C provides 5V input/output
- 3.3V regulator: 700mA max output
- Battery: 3.7V LiPo to BAT+/BAT- on back (3.0V-4.2V safe range)
- Charge LED (red): on=charging, off=complete
- All GPIO are 3.3V logic -- NOT 5V tolerant

## Sense Variant Pin Usage

Camera and mic GPIOs are routed through the B2B expansion connector, not the
main castellated pads. These GPIOs are NOT available on the base board.

- Camera (OV2640): GPIO10-18, 38-40, 47-48 (Sense B2B only)
  - Camera I2C: SIOD=GPIO40, SIOC=GPIO39
- PDM Mic: CLK=GPIO42 (shared with D11), DATA=GPIO41 (shared with D12)
  - When mic is active, D11/D12 are unavailable for general use
- SD Card: CS=D2(GPIO3), CLK=D8(GPIO7), MISO=D9(GPIO8), MOSI=GPIO10(Sense B2B)
  - Shares SPI bus with D8-D10; GPIO10 for SD MOSI comes via B2B, not main header

## Reserved GPIOs

GPIO26-32 are used internally for flash/PSRAM (OPI) and are NOT available.
GPIO0 and GPIO46 are strapping pins that affect boot mode -- do not drive
these externally unless you understand the boot sequence.
