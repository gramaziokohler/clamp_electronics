# clamp_electronics
Electronics for remote controlled robotic actuators (clamps). 

This repo is part of the [Robotic Assembled Timber Structures with Integral Timber Joints](https://github.com/gramaziokohler/integral_timber_joints) project. 

## Repo folder structure

This repository hold the following files:

- **/xx_Description** - Eagle schematics and board designs for a specific controller design
- **/eagle_library** - stores custom eagle libraries from third-party or created by myself
- **/doc** - Electronics modules and other components documentation from original manufactures.

## Design Goals

The goal of the clamp controller is to be able to achieve the following high-level functions: 

- Communicate wirelessly with a radio base station
  - Receive commands
  - Report status
  - Report a jammed stop during move
- Control 1 or 2 motors for the clamp's main linear movement
  - Positional Control
  - Follow a trapezoidal motion profile
- Operate on 3 or 4-cell Li-Po Battery power
- Monitor jamming conditions of the clamp
- Monitor sensors (if any, such as loadcells)
- Monitor end / homing switch
- Monitor pneumatic autoswitch
- Monitor battery voltage

## Controller Design

Not all designs implemented the full list of design goals.

### [01_SerialController](/01_SerialController/01_SerialController.md)

This controller receives command from Serial Tx Rx pins.

Two load cell can be connected via two HX711 Analog-to_Digital Module.

The design supports two DC motors with *single* channel encoder. The shaft rotation direction is inferred from the direction of programmed movement. (This design is later proved to be imprecise)

### [02_RadioPIDController](02_RadioPIDController/02_RadioPIDController.md)

This controller interfaces the CC1101 radio directly via Hardware SPI on Arduino Nano. It can receive and respond to commands from either USB Serial or from the Radio.

The hardware and pin out supports two motors being PID controlled with two-channel encoder feedback.

### [03_RadioPIDControllerV2](03_RadioPIDControllerV2/03_RadioPIDControllerV2.md)

This controller is an improvement of the 02_RadioPIDController with the intent to improve the following aspects:

- Better DC power regulation to avoid digital blackout
- Ability to support a two-motor firmware or single-motor (with added features) firmware.
- 1 or 2 LED output with onboard series resistor

### [10_ESP32CAMAdapter](10_ESP32CAMAdapter/10_ESP32CAMAdapter.md)

This an adapter board for connecting AIThinker ESP32-CAM module.

## Sub-systems and Electronic Module Documentation

### Motor Driver

[Motor Driver XY160D](doc/motor_driver/motor_driver_XY160D.md)

This H-Bridge Bi-Directional MOSFET motor driver is chosen due to its high rated current (7A constant, 50A peak).  

- Other drivers such as L298N offers low output current (L298N only 2A constant output 3A peak per channel) 
- This driver has a simple IN1 + IN2 + ENA interface which is easy to interface. 
- PWM and Bidirectional operation is necessary for position control.

### Radio

[Details of CC1101 Radio Module](doc/radio/CC1101_Radio.md)

This CC1101 radio module is chosen because it is the most available sub-GHz packet based radio.

- The sub-GHz frequency is better at going around obstacles in a construction environment.
- ISM bands that are free to use.
- The highly integrated radio transceiver chip on a module is easy to use and interface. 
- Existing Arduino compatible library exists.

Radio frequency / channel / sync word and it's operation is controlled by software and are documented in firmware repo.

### MCU

The Arduino Nano (ATmega328 + new bootloader) is chosen for its small size, low cost and protoboard friendly pin layout. The Nano do not have a lot of IO available but is barely enough for a 2 motor controller.

[Arduino Nano V3 Pinout](http://lab.dejaworks.com/arduino-nano-pinouts/) ( [Arduino.cc Nano Page](https://store.arduino.cc/arduino-nano) )

### Load Cell

A 4-wire load cell can be used to dynamically measure the pull force of the actuator. Such load cell can be interfaced to the Arduino via a AD Converter designed for load cell measurement.

[Details of the HX711 Load Cell A/D Module](/doc/load_cell/load_cell.md)

The HX711 module was selected due to its compact size, low cost and ready-to-use library. Measuring frequency is 80Hz.

### Battery Voltage Regulation for controller

The fluctuating battery voltage for a 4-cell Li-Po is between 12.8V to 16.8V. This needs to be regulated to stable 5V DC for the digital circuitry.

[Details and calculation of LM7805 option](doc/voltage_regulation/linear_regulator.md)

### Battery Voltage Sense

[Details and calculation of voltage divider](doc/battery_sense/Battery_Voltage_Sensing.md)

### Battery Cable Harness

A Y cable is necessary to connect the Li-Po Battery to both the motor driver and the controller Battery. 

**Male XT60 Connector** at the battery side

**2x Female Phoenix Terminal Block Plug** (Phoenix 1757019 - MSTB 5.08 picth) at controller side.



------



## Peripheral Devices

The choice of DC motor and Li-Po Battery is flexible from the perspective of the controller electronics. As long as their specification is within allowable range defined below:

### DC Motor

The chosen DC motor should be rated 12V. Other ratings might work as long as overheat is not an issue and sufficient torque is produced.

### Hall Effect Sensor

Two phase hall effect shaft encoder should be used for positional feedback. The output of the encoder should ideally be 5V TTL logic. 

Should the motor have a gearbox, the shaft encoder should be attached to the motor shaft (not the gearbox output shaft) for better resolution.

Sensor resolution should be around 500 - 1000 steps per 1mm clamp linear output.

### Li-Po Battery

**4-cell** Li-Po battery is chosen for the following reasons:

- High power density for starting DC motor
- High energy density to save space and weight
- 14.8V - 16.8V voltage match well with 12V DC motor.

**1000mAh** or above for reasonable use time.

**XT60 Connector** is conventional

**Voltage Assumption for calculation**: We assume a fully charged 4-cell battery to have **16.8V (@4.2V)**, and stop using the battery at **14.8V (@3.7V)**  , although absolute minimum is **14.0V (@3.5V)**

Note: 3-cell battery will also operate fine but at reduced torque

Credits
-------------

This repository was created by Pok Yin Victor Leung <leung@arch.ethz.ch> [@yck011522 ](https://github.com/yck011522) at [@gramaziokohler](https://github.com/gramaziokohler)

