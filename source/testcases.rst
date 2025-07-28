Test Cases and Observations
===========================

Hardware Test Cases
-------------------


I²C Bus Verification
^^^^^^^^^^^^^^^^^^^^

.. list-table::
   :header-rows: 1
   :widths: 10 30 40 20

   * - ID
     - Test Case
     - Description
     - Expected Result
   * - H1
     - I²C Address Probe
     - Use i2cdetect to verify device at 0x68
     - Device appears at correct address
   * - H2
     - I²C Read/Write Basic
     - Access registers using i2cget/i2cset
     - Read/write succeeds


**Result:**
~~~~~~~~~~~

.. literalinclude:: /_static/logs/HW_1&2log.txt
   :language: none
   :caption: I²C Bus Verification

Oscillator & Clock Validation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
   :header-rows: 1
   :widths: 10 30 40 20

   * - ID
     - Test Case
     - Description
     - Expected Result
   * - H3
     - Clock Output Stability
     - Observe 32.768 kHz CLKOUT (if routed)
     - Stable signal within ±20 ppm

**Result:**  
~~~~~~~~~~~

.. literalinclude:: /_static/logs/HW3log.txt
   :language: none
   :caption: Measured CLKOUT output captured during testing.
     

Power Domain & Backup Supply
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
   :header-rows: 1
   :widths: 10 30 40 20

   * - ID
     - Test Case
     - Description
     - Expected Result
   * - H4
     - VCC Loss Simulation
     - Cut VCC, keep VBAT active
     - RTC continues using backup
   * - H5
     - VBAT Fail Simulation
     - Remove VBAT, power VCC
     - RTC stops; VLOW flag set
   * - H6
     - RTC Reset on Dual Loss
     - Remove both VCC and VBAT
     - RTC resets to default time

**Result:**  
~~~~~~~~~~~

.. literalinclude:: /_static/logs/HW4_5_6.txt
   :language: none
   :caption: Power Domain & Backup Supply.


Software Test Cases
-------------------


Device Tree & Driver Verification
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. list-table::
   :header-rows: 1
   :widths: 10 30 40 20

   * - ID
     - Test Case
     - Description
     - Expected Result
   * - S1
     - Device Tree Overlay
     - Configure RTC node in DTS
     - RTC detected as /dev/rtc0
   * - S2
     - Driver Load Test
     - Boot with RTC node present
     - `rtc-m41t80` driver loads
   * - S3
     - DTBO Hotplug
     - Load overlay via configfs
     - RTC node appears in sysfs


**Result:**  
~~~~~~~~~~~

.. literalinclude:: /_static/logs/SW1_2_3log.txt
   :language: none
   :caption: Device Tree & Driver Verification.


Functional RTC Tests
^^^^^^^^^^^^^^^^^^^^     
  
.. list-table::
   :header-rows: 1
   :widths: 10 30 40 20

   * - ID
     - Test Case
     - Description
     - Expected Result
   * - S4
     - Time Set/Get
     - Use hwclock to set and read time
     - Time read equals time set
   * - S5
     - Kernel Sync Test
     - Sync RTC to system, reboot
     - Time restored from RTC

**Result:**  
~~~~~~~~~~~

.. literalinclude:: /_static/logs/SW4_5log.txt
   :language: none
   :caption: Functional RTC Tests.
  

Status and Control Register Tests
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


.. list-table::
   :header-rows: 1
   :widths: 10 30 40 20

   * - ID
     - Test Case
     - Description
     - Expected Result
   * - S6
     - OSF Bit Test
     - Simulate power loss
     - OSF bit set on power restore
   * - S7
     - Bit‑Level Access
     - Modify individual bits
     - Bits toggle correctly


**Result:**
~~~~~~~~~~~

.. literalinclude:: /_static/logs/SW6_7log.txt
   :language: bash
   :caption: Status and Control Register Tests.


Boundary and Stress Tests
^^^^^^^^^^^^^^^^^^^^^^^^^
     
.. list-table::
   :header-rows: 1
   :widths: 10 30 40 20

   * - ID
     - Test Case
     - Description
     - Expected Result
   * - S8
     - Burst I²C Access
     - Continuous read/write loop
     - No data loss or failure
   * - S9
     - Long Uptime Test
     - Run for 24–72 hours
     - Drift within spec
   * - S10
     - Kernel Panic Recovery
     - Crash and reboot
     - RTC time retained

**Result:**
~~~~~~~~~~~

.. literalinclude:: /_static/logs/SW9_10_11log.txt
   :language: bash
   :caption: Boundary and Stress Tests.
    

PPM Compensation Test
---------------------

.. literalinclude:: /_static/logs/rtc_ppm_compensation_test.txt
   :language: none
   :caption: PPM Compensation Log

