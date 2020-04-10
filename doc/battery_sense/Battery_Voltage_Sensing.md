# Battery Voltage Sensing

Battery voltage is monitored with one of the analog input on Arduino via a voltage divider.

Below is a divider schematic showing R1 and R2.

![voltage_divider](C:\Users\Victor\Documents\GitHub\clamp_electronics\doc\battery_sense\voltage_divider.jpg)

## Calculation

Voltage Divider Calculation: http://www.ti.com/download/kbase/volt/volt_div3.htm (E24 values)

| LiPo Cells | Charged Voltage | Empty Voltage | R1 (Ω)   | R2 (Ω)   | Power Diss @ Charged Voltage (mW) | Converted Voltage |
| ---------- | --------------- | ------------- | -------- | -------- | --------------------------------- | ----------------- |
| 1          | 4.2             | 3.7           | 0        | x        | 0                                 |                   |
| 2          | 8.4             | 7.4           | 680      | 1000     | 42                                | 5.0               |
| 3          | 12.6            | 11.1          | 5100     | 3300     | 19                                | 4.95              |
| 4          | 16.8            | 14.8          | **4300** | **1800** | 46                                | 4.96              |
| 4          | 16.8            | 14.8          | **4700** | **2000** | 42                                | 5.01              |

Note: The bold values can be used.

Empty battery has about 3.7/4.2 88% of the fully charged voltage. With the 1024 steps AnalogRead() on Arduino ADC, the **theoretical resolution of the capacity measurement is 121 steps.**

