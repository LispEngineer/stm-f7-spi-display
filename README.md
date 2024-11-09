# STM32 SPI Display Demo

* Author: Douglas P. Fields, Jr.
* Date: 2024-11-09

# Software References

* [STM ILI9341 Display](https://github.com/afiskon/stm32-ili9341?tab=readme-ov-file)
* STM32 Cube IDE 1.16

# Hardware

* Nucleo F767ZI
* [ILI9341](https://www.pjrc.com/store/display_ili9341_touch.html)

Others:

* [ST7796S](http://www.lcdwiki.com/4.0inch_SPI_Module_ST7796)

# Nucleo-144 Pinout

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

# Doug's notes

* This is really slow
  * Area fills call the HAL 2 bytes at a time
  * There is no DMA or sending buffer
* The image dump is really fast due to a single HAL call
* I don't readily see how this can be easily done with DMA
  given the need to toggle the CS and CD GPIOs occasionally
  and in sync with the SPI data  
  
  
* TODO

* Figure out how to use 8-bit color so we can double the speed
  of the I/O we do with bitmaps