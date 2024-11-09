


# References

* [STM ILI9341 Display](https://github.com/afiskon/stm32-ili9341?tab=readme-ov-file)

# Hardware

* [ILI9341](https://www.pjrc.com/store/display_ili9341_touch.html)
* [ST7796S](http://www.lcdwiki.com/4.0inch_SPI_Module_ST7796)

# Nucleo Pinout

D13 PA5  SPI1_SCK
D12 PA6  SPI1_MISO
D51 PD7  SPI1_MOSI
D10 PD14 SPI1_DC
D9  PD15 SPI1_CS
D8  PF12 SPI1_RESET

## Display connections

* VCC - 5V
* GND - GND
* CS - GND (Chip always selected)
* Reset - 3.3V (Never in reset)
* LED - 3.3V (backlight, instructions say use 100 ohm resistor)

# Software Notes

Chip configuration
* NVIC
  * SPI1 Global Interrupt: Enable
* SPI1