German Team Communication
=========================

Summary
-------

A detailed report was sent to the PHYTEC German team describing all the steps taken to investigate the RTC drift issue on the RV-4162-C7 connected to the AM335x SOM. The goal was to understand whether the delay was due to RTC design, Linux driver limitations, or hardware behavior.

Recommendations from German Team
--------------------------------

The following key suggestions were received:

- Verify whether `hwclock -s -f /dev/rtc0` correctly updates the seconds field (we tested this; the issue persisted).
- Consider using NTP synchronization to eliminate drift; however, this was ruled out due to lack of network/internet in the client’s deployment.
- Measure the 32.768 kHz CLKOUT output to assess oscillator frequency drift.
- Apply software-based frequency compensation as per **Section 4.2** of the RV-4162-C7 Application Manual.
- Calculate ppm error based on seconds/day drift and apply corresponding positive frequency compensation.

Example Commands: 
^^^^^^^^^^^^^^^^^

.. code-block:: bash

   i2cget -f -y 1 0x68 0x08
   i2cset -f -y 1 0x68 0x08 0x20

This sets:

- CLKOE = 1
- FD = 0001 → 32.768 kHz
- CAL = 5 → positive calibration to reduce delay


