Software Overview
====================

RTC Driver
----------

- Linux driver: rtc-m41t80
- Device node: /dev/rtc0

Key Commands
------------

.. code-block:: bash

 Set system time: date MMDDhhmmYYYY.ss
 Write to RTC: hwclock -w -f /dev/rtc0
 Read from RTC: hwclock -r -f /dev/rtc0
 Sync RTC to system: hwclock -s -f /dev/rtc0
