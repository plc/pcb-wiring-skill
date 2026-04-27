# XIAO nRF52840

Source: https://wiki.seeedstudio.com/XIAO_BLE/

## Front (USB North)

```
                      +--USB-C--+
                      | [R]     |
  P0.02  A0  D0 -|o         o|- 5V
  P0.03  A1  D1 -|o         o|- GND
  P0.28  A2  D2 -|o         o|- 3V3
  P0.29  A3  D3 -|o  XIAO   o|- D10 MOSI P1.15
  P0.04 SDA  D4 -|o  nRF    o|- D9  MISO P1.14
  P0.05 SCL  D5 -|o  52840  o|- D8  SCK  P1.13
  P1.11  TX  D6 -|o         o|- D7  RX   P1.12
                      | [ANT]   |
                      +---------+
```

## Back (USB North, board flipped)

```
              +--USB-C--+
              |         |
         CLK -|o       o|- DIO
         GND -|o       o|- RST
              |o       o|- BAT-
              |        o|- BAT+
              |         |
          NFC -o---------+
```

## Legend

- [R] Reset button
- [ANT] Bluetooth PCB antenna
- CLK/DIO = SWD debug
- RST = Reset
- BAT+/BAT- = 3.7V LiPo
- NFC = P0.09/P0.10
- User LED (RGB): Red=P0.26, Green=P0.30, Blue=P0.06 (active LOW)
- Charge LED: P0.17
- 3.3V logic, NOT 5V tolerant
- 3V3 regulator: 700mA max
- No bottom pads on standard model

## Bus Defaults

- I2C: SDA=D4(P0.04), SCL=D5(P0.05)
- SPI: SCK=D8(P1.13), MISO=D9(P1.14), MOSI=D10(P1.15)
- UART: TX=D6(P1.11), RX=D7(P1.12) -- Serial1; Serial0=USB CDC

## Sense Variant

- IMU (LSM6DS3TR-C): internal I2C, power=P1.08, interrupt=P0.11 (not on header)
- PDM Mic: CLK=P1.00, DATA=P0.16 (not on header)

## Battery ADC

Read battery via P0.31 (AIN7). Set P0.14 LOW first to enable divider.
Leaving P0.14 HIGH while reading risks damage to P0.31.

## Pin Numbering

Arduino A0-A5 do not match nRF AIN channels:
A0=AIN0, A1=AIN1, A2=AIN4, A3=AIN5, A4=AIN2, A5=AIN3.
Use Arduino labels in code, not AIN numbers.
