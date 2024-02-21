# T2402_ATtiny_Solutions
My initial interest in the ATtiny85 is to build a combined power off circuit and a hardware watchdog. When learning more about the ATtiny85 I realized that this small chip can also provide the EEPROM that I have been lacking in some project. THe goal is to design a small PCB that I can use in different projects especially when using prototype boards.  This watchdog that I have started to call "edog" (energy saving watchdog). I could have adde stille one "e"for the EEPROM but I decided the edog sounds better.
## Requirements
* Watchdog with adjustable timeout, power off->on or reset
* Energy saving with adjustable sleep time
* Low sleep current, target was 20uA
* EEPROM storage for the main MCU

## Programming and Test Setup
You can probably buy assembled programmers for the ATtiny85 but I did not want to wait and also I wanted to use a zero-force socket I had in my stash. The 20 pin socket also provided a practical socket when testing the software. Moving the chip back and forth may sound clumpsy and very old school. It happened that the chip was in wrong position but this was quickly noticed and fixed. To be able to test the I2C slave functions I had to implement a I2C master application.  For this purpose I used an Arduino Nano.
In additon the the basic test setup I was also using a Kingst LA2016 Logic Analyzer. This proved to be fully 
irreplaceable. I was also using the Nordic Semiconductor Power Profiler Kit II to measure the current consumption.

## Hardware

## Software

## Results
