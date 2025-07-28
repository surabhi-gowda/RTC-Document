Tools and Utilities
===================

This section outlines the key software and hardware tools used throughout the RTC validation and drift analysis process on the AM335x platform with the RV-4162-C7 RTC.

Hardware Tools
--------------

- **Oscilloscope**  
  Used to observe and verify:
  - CLKOUT signal stability and frequency (32.768 kHz)
  - I²C bus signal quality (SCL/SDA waveforms)
  - Glitches or timing violations

- **Multimeter**  
  Used to measure:
  - VCC and VBAT voltages
  - Signal line idle states (pull-up verification)
  - Decoupling capacitor voltage stability

- **Thermal Chamber / Heat Gun / Ice Spray**   
  Used to simulate temperature extremes (-40 °C to +85 °C) and assess drift due to thermal influence.

- **Power Supply + Current Monitor** *(Optional)*  
  Used to simulate VCC/VBAT loss and monitor RTC power consumption under different conditions.

- **Logic Analyzer** *(Optional)*  
  Helpful in decoding I²C communication for detailed debugging or in noisy environments.


Software Tools
--------------

- **i2c-tools** (`i2cdetect`, `i2cget`, `i2cset`)  
  Command-line tools for direct I²C register access. Used for:
  - Probing the RTC (0x68)
  - Reading and writing control/status/calibration registers

- **hwclock**  
  Linux utility for reading from and writing to `/dev/rtcX`. Used to:
  - Set and read RTC time
  - Sync system clock from RTC and vice versa

- **Linux sysfs and devfs interfaces**  
  - `/sys/class/rtc/rtc0/`
  - `/dev/rtc0`  
  Used for alarm testing, wakealarm configuration, and direct user-space interaction with RTC.

- **Scripting Tools**  
  - Bash / Cron for long-duration time logging and drift analysis.
  - Python (optional) for log parsing and ppm drift calculation.

