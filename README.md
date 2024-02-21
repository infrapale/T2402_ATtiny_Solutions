# T2402_ATtiny_Solutions
My initial interest in the ATtiny85 is to build a combined power off circuit and a hardware watchdog. When learning more about the ATtiny85 I realized that this small chip can also provide the EEPROM that I have been lacking in some project. The goal is to design a small PCB that I can use in different projects especially when using prototype boards.  This watchdog that I have started to call "edog" (energy saving watchdog). I could have added still one "e" for the EEPROM but I decided the edog sounds better.

## My ATtiny85 Repositories
* https://github.com/infrapale/T2402_ATtiny85_Work_Files
* https://github.com/infrapale/T2402_edog_master_test


## Requirements
* Watchdog with adjustable timeout, power off->on or reset
* Energy saving with adjustable sleep time
* Low sleep current, target was 20uA
* EEPROM storage for the main MCU

## Programming and Test Setup
You can probably buy assembled programmers for the ATtiny85 but I did not want to wait and also I wanted to use a zero-force socket I had in my stash. The 20-pin socket also provided a practical socket when testing the software. Moving the chip back and forth may sound clumsy and very old school. It happened that the chip was in wrong position, but this was quickly noticed and fixed. To be able to test the I2C slave functions I had to implement a I2C master application. For this purpose, I used an Arduino Nano.

In addition to the basic test setup, I was also using a Kingst LA2016 Logic Analyzer. This proved to be fully irreplaceable. I was also using the Nordic Semiconductor Power Profiler Kit II to measure the current consumption.

![testing](/images/Test_Setup.png)

## Hardware
### Programmer

The programmer is a slightly modified version of ATTiny programmers found on the web. I was using a Arduino Nano to get a compact programming and testing setup.

![testing](/images/ATtiny85_programmer.png)

### Test Circuit
![testing](/images/ATtiny85_Test_circuit.png)


## Software
The edog software is implementing following main functions:
* Receive watchdog timeout from I2C
* Receive watchdog clear command from I2C
* Receive sleep time from I2C
* Receive goto sleep command from I2C

The edog software is built on following libraries
* TinyWires.h    I2C implementation for ATtiny
* tinysnore.h    Sleep function for ATTiny
* EEPROM.h       Arduino EEPROM support

### EEPROM Communication
![testing](/images/edog_EEPROM_write_read.png)
![testing](/images/EEPROM_Save_I2C.png)
![testing](/images/EEPROM_Load_I2C.png)

## Results
So far I have not achieved the target 20uA sleep current. The sleep current is now 70uA which is not too bad when running on AA batteries. 2000mAh/70uA = 28571 hours = 1190 days
When running the ATtiny85 in this setup with 3.3V is consuming about 1mA.
 
![testing](/images/Sleep_Current.png)

## Links
* https://github.com/rambo/TinyWire
* https://www.tastethecode.com/introducing-the-attiny-device-pcb-i2c-slave-devices

* https://en.wikipedia.org/wiki/I%C2%B2C
* https://learn.sparkfun.com/tutorials/sparkfun-qwiic-button-hookup-guide
*https://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-2586-AVR-8-bit-Microcontroller-ATtiny25-ATtiny45-ATtiny85_Datasheet.pdf

## Conclusion
Again I spent more time than anticipated on the edog project. Many of the issues were related to the I2C slave functions. Without the logic analyzer I would still be struggling. The master code I implmented to test the solution was at least 50% of the effort spent. Initially I was "manually" sending messages, but to complete the testing I had to refactor the code and improve the abstraction level
