---
title: 'Arduino & Serial Peripheral Interface (SPI)'
description: 'Serial Peripheral Interface (SPI) is a synchronous serial data protocol used by microcontrollers for communicating with one or more peripheral devices quickly over short distances.'
author: Arduino
tags: [SPI]
difficulty: 'intermediate'
---

>This article was revised on 2021/11/18 by Karl Söderby.

***Controller/peripheral is formerly known as master/slave. Arduino no longer supports the use of this terminology. See the table below to understand the new terminology:***

| Master/Slave (OLD)         | Controller/Peripheral (NEW)          |
| -------------------------- | ------------------------------------ |
| Master In Slave Out (MISO) | Controller In, Peripheral Out (CIPO) |
| Master Out Slave In (MOSI) | Controller Out Peripheral In (COPI)  |
| Slave Select pin (SS)      | Chip Select Pin (CS)                 |

---

## SPI Library

The SPI Library is included in every Arduino core/platform, so you do not need to install it externally. You can read more about SPI functions in the links below:

- [SPI Library](https://www.arduino.cc/en/reference/SPI)
- [GitHub (ArduinoCore-avr)](https://github.com/arduino/ArduinoCore-avr/tree/master/libraries/SPI)

## Serial Peripheral Interface (SPI)

With an SPI connection there is always one Controller device (usually a microcontroller) which controls the peripheral devices. Typically there are three lines common to all the devices:

- **CIPO (Controller In Peripheral Out)** - The Peripheral line for sending data to the Controller
- **COPI (Controller Out Peripheral In)** - The Controller line for sending data to the peripherals
- **SCK (Serial Clock)** - The clock pulses which synchronize data transmission generated by the Controller
and one line specific for every device
- **CS (Chip Select)** - the pin on each device that the Controller can use to enable and disable specific devices.
When a device's Chip Select pin is low, it communicates with the Controller. When it's high, it ignores the Controller. This allows you to have multiple SPI devices sharing the same CIPO, COPI, and CLK lines.

To write code for a new SPI device you need to note a few things:

- What is the maximum SPI speed your device can use? This is controlled by the first parameter in SPISettings. If you are using a chip rated at 15 MHz, use 15000000. Arduino will automatically use the best speed that is equal to or less than the number you use with SPISettings.
- Is data shifted in Most Significant Bit (MSB) or Least Significant Bit (LSB) first? This is controlled by second SPISettings parameter, either MSBFIRST or LSBFIRST. Most SPI chips use MSB first data order.
- Is the data clock idle when high or low? Are samples on the rising or falling edge of clock pulses? These modes are controlled by the third parameter in SPISettings.
- The SPI standard is loose and each device implements it a little differently. This means you have to pay special attention to the device's datasheet when writing your code.

Generally speaking, there are four modes of transmission. These modes control whether data is shifted in and out on the rising or falling edge of the data clock signal (called the clock phase), and whether the clock is idle when high or low (called the clock polarity). The four modes combine polarity and phase according to this table:

| Mode      | Clock Polarity (CPOL) | Clock Phase (CPHA) | Output Edge | Data Capture |
| --------- | --------------------- | ------------------ | ----------- | ------------ |
| SPI_MODE0 | 0                     | 0                  | Falling     | Rising       |
| SPI_MODE1 | 0                     | 1                  | Rising      | Falling      |
| SPI_MODE2 | 1                     | 0                  | Rising      | Falling      |
| SPI_MODE3 | 1                     | 1                  | Falling     | Rising       |

Once you have your SPI parameters, use `SPI.beginTransaction()` to begin using the SPI port. The SPI port will be configured with your all of your settings. The simplest and most efficient way to use SPISettings is directly inside `SPI.beginTransaction()`. For example:

```arduino
SPI.beginTransaction(SPISettings(14000000, MSBFIRST, SPI_MODE0));
```

If other libraries use SPI from interrupts, they will be prevented from accessing SPI until you call `SPI.endTransaction()`. The SPI settings are applied at the begin of the transaction and `SPI.endTransaction()` doesn't change SPI settings. Unless you, or some library, calls beginTransaction a second time, the setting are maintained. You should attempt to minimize the time between before you call `SPI.endTransaction()`, for best compatibility if your program is used together with other libraries which use SPI.

With most SPI devices, after `SPI.beginTransaction()`, you will write the Chip Select pin LOW, call `SPI.transfer()` any number of times to transfer data, then write the CS pin HIGH, and finally call `SPI.endTransaction()`.

For more on SPI, see [Wikipedia's page on SPI](http://en.wikipedia.org/wiki/Serial_Peripheral_Interface_Bus#Mode_Numbers).

## Tutorials

- [Extended SPI Library Usage with the Arduino Due](/tutorials/due/due-extended-spi)
- [Introduction to the Serial Peripheral Interface](/tutorials/generic/introduction-to-the-serial-peripheral-interface)
- [Digital Potentiometer Control (SPI)](/tutorials/communication/DigitalPotControl)
- [Barometric Pressure Sensor (SPI)](/tutorials/communication/BarometricPressureSensor)