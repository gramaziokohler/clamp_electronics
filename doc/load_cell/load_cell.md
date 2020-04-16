# HX711 Load Cell A/D Module

There are different HX711 module on the market. Notably the Sparkfun version and this brand-less version. Note that pin arrangement is not identical. 

I choose this brand-less option simply because of lower cost.

![HX711_module](C:\Users\Victor\Documents\GitHub\clamp_electronics\doc\load_cell\HX711_module.jpg)

## Specification of HX711

 [Data Sheet of Avia Semiconductor HX711](HX711.pdf)

**Resolution:** 24bit

**Measurement frequency:**10Hz / 60Hz (selectable)



## Pin Connection

Between Arduino and HX711 module:

| Label on module | Arduino Pin               | Notes     |
| --------------- | ------------------------- | --------- |
| VCC             | +5V                       | Power     |
| GND             | GND                       | Power     |
| DT              | Software SPI (Any IO Pin) | SPI Data  |
| SCK             | Software SPI (Any IO Pin) | SPI Clock |

____

Between HX711 module and load cell:

| Label on module | Load Cell Wire | Cable Color (most of the time) |
| --------------- | -------------- | ------------------------------ |
| E+              | Excitation +   | Red                            |
| E-              | Excitation -   | Black                          |
| A-              | Amplifier -    | Green                          |
| A+              | Amplifier +    | White                          |
| B-              | Not Connected  |                                |
| B+              | Not Connected  |                                |
| GND             | Shield         | Wire or foil shield            |

