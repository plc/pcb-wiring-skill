# XIAO ESP32-S3

Source: https://wiki.seeedstudio.com/xiao_esp32s3_getting_started/

## Front (USB North)

```
                         +---USB-C---+
                         | [R]   [B] |
  TOUCH1 GPIO1  A0  D0 -|o         o|- 5V
  TOUCH2 GPIO2  A1  D1 -|o         o|- GND
  TOUCH3 GPIO3  A2  D2 -|o         o|- 3V3
  TOUCH4 GPIO4  A3  D3 -|o  XIAO   o|- D10 A10 MOSI GPIO9  TOUCH9
  TOUCH5 GPIO5 SDA  D4 -|o ESP32S3 o|- D9  A9  MISO GPIO8  TOUCH8
  TOUCH6 GPIO6 SCL  D5 -|o         o|- D8  A8  SCK  GPIO7  TOUCH7
         GPIO43 TX  D6 -|o         o|- D7  RX       GPIO44
                         |   [ANT]   |
                         +-o-------o-+
                         D11       D12
                        (left)   (right)
                         A11       A12
                       GPIO42    GPIO41
                      TOUCH12   TOUCH13
```

## Back (USB North, board flipped)

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

## Legend

- [R] Reset  [B] Boot (GPIO0, hold during reset for download mode)
- [ANT] U.FL WiFi/BT antenna connector
- [ThPAD] Thermal/ground pad
- MTDO/MTDI/MTCK/MTMS = JTAG
- BAT+/BAT- = 3.7V LiPo (3.0-4.2V)
- D+/D- = USB data
- User LED: GPIO21 (active low)
- Charge LED (red): top-left near USB
- 3.3V logic, NOT 5V tolerant
- 3V3 regulator: 700mA max

## Bus Defaults

- I2C: SDA=D4(GPIO5), SCL=D5(GPIO6)
- SPI: SCK=D8(GPIO7), MISO=D9(GPIO8), MOSI=D10(GPIO9)
- UART: TX=D6(GPIO43), RX=D7(GPIO44) -- Serial1; Serial0=USB CDC

## Sense Variant

- Camera (OV2640): GPIO10-18, 38-40, 47-48 via B2B connector (not on header)
- PDM Mic: CLK=GPIO42 (D11), DATA=GPIO41 (D12) -- when active, D11/D12 unavailable
- SD Card: CS=D2, CLK=D8, MISO=D9, MOSI=GPIO10(B2B) -- shares SPI bus
