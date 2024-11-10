# STM32 SPI Display Demo

* Author: [Douglas P. Fields, Jr.](mailto:symbolics@lisp.engineer)
* Date: 2024-11-09
* Copyright 2024 Douglas P. Fields, Jr.
* License: [MIT](LICENSE) (as per original SPI code)
  * Portions from STM/STM code generation

Goals:
* Make an ILI9341 display work on a Nucleo-F767ZI board.
* Improve performance of original code

# Software Used

* [STM ILI9341 Display](https://github.com/afiskon/stm32-ili9341?tab=readme-ov-file)
  by Aleksander Alekseev under [MIT License](https://opensource.org/license/mit)
* STM32 Cube IDE 1.16

# Hardware

* Nucleo F767ZI
* [ILI9341](https://www.pjrc.com/store/display_ili9341_touch.html)

Other possibilities:

* [ST7796S](http://www.lcdwiki.com/4.0inch_SPI_Module_ST7796)

# Nucleo-144 Pinout

See STM UM1974 Rev 10 page 32 section 6.13

```
D13 PA5  SPI1_SCK
D12 PA6  SPI1_MISO
D51 PD7  SPI1_MOSI
D10 PD14 SPI1_DC
D9  PD15 SPI1_CS
D8  PF12 SPI1_RESET
```

## Display non-data connections

* VCC - 5V
* GND - GND
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
  
# TODO

* Figure out how to use 8-bit color so we can double the speed
  of the I/O we do with bitmaps
  * DOesn't seem to be a way to do this
* Use a smaller pixel buffer than 320x240x2 bytes (150k)
  * Maybe use an Nk buffer and loop through it when needed
  * But at least big enough for a decent font size like 16x26
    which is 832 bytes
  * I was thinking more like 16k or 8k pixels
    * This would require 19 writes to blank the whole screen
* Rewrite this all with queues and DMA
  * Have reusable buffers
  * Have callbacks when requests are completed