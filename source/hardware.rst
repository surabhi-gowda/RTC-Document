Hardware Overview
=================

RTC Device
----------

- Model: RV-4162-C7
- Interface: I²C (address 0x68)
- Crystal: Integrated 32.768 kHz crystal oscillator.
- Features: Frequency offset compensation, alarm, watchdog, programmable CLKOUT.
- Compensation: Supports frequency offset compensation (±20 ppm).
- Accuracy: ±20 ppm, compensatable to ±2 ppm 
- Temperature Range: –40 °C to +85 °C, typical drift ±5 ppm at 25 °C
- Aging: ≤3 ppm first year, ≤1 ppm/year

Power Section
-------------

- RTC powered via VCC_3V3 (main supply) or VBAT (backup battery)
- Automatic switchover to VBAT on VCC loss.
- Power integrity checked
- VCC and VBAT stability verified during operation.
- Capacitor on VCC: 1 uF originally, replaced with 10 uF as part of tests → no significant impact on drift.
- Diode protection (e.g. BAT42) present for battery input.

Power Supply Diagram
--------------------

The diagram below shows the VCC and VBAT power domains feeding the RTC.

.. image:: /_static/rtc_power_flow.png
   :alt: RTC VCC/VBAT Block
   :width: 80%
   :align: center


I²C & Signal Integrity
----------------------

- Pull-up resistors: 4.7 kΩ
- SCL and SDA lines connected to AM335x I2C controller
- External pull-up resistors: 4.7 kΩ on SCL/SDA, design-verified
- No pull-down resistors present


