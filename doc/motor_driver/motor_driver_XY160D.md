# XY-160D motor driving board

**Motor Power Input Voltage** DC 6.5V - 27V

**Digital Power Input Voltage** DC 5V

**Number of Channels:** 2

**Max continuous output current:**  7A (Per Channel)

**Peak output current**: 50A

**PWM frequency range** 0-10 kHz (PWM signal at ENA input is used to regulate speed)

**Minimum pulse width:** 5us.

**Control signal Level (Compatible 3.3V/5V)**

**Logic High (H):** DC 3.0 ~ 6.5V

**Logic Low (L):** DC0 ~ 0.8V

| Pin Function                    | Label          | Connection          |
| ------------------------------- | -------------- | ------------------- |
| Drive Power Input +ve           | 9-24V          | Battery Positive    |
| Drive Power Input -ve           | PGND           | Battery Negative    |
| Power Output - Channel 1 +ve    | OUT1           | Channel 1 Motor +ve |
| Power Output - Channel 1 -ve    | OUT2           | Channel 1 Motor -ve |
| Power Output - Channel 2 +ve    | OUT3           | Channel 2 Motor +ve |
| Power Output - Channel 2 -ve    | OUT4           | Channel 2 Motor -ve |
| Digital Power Input +ve         | +5V            | Arduino 5V          |
| Digital Power Input -ve         | GND            | Arduino Ground      |
| Digital Input - Channel 1 - 1   | IN1            | Arduino GPIO        |
| Digital Input - Channel 1 - 2   | IN2            | Arduino GPIO        |
| Digital Input - Channel 2 - 1   | IN3            | Arduino GPIO        |
| Digital Input - Channel 2 - 2   | IN4            | Arduino GPIO        |
| Digital Input - Channel 1 Speed | ENA (near IN1) | Arduino GPIO (PWM)  |
| Digital Input - Channel 2 Speed | ENA (near IN3) | Arduino GPIO (PWM)  |

Note: Motor +ve and -ve denote when the motor spins according to Right Hand Rule. (a.k.a. CCW when viewed from output end.)



## Control Truth Table

| ENA  | IN1  | IN2  | OUT1 OUT2 Effect             |
| ---- | ---- | ---- | ---------------------------- |
| x    | L    | L    | Short (Breaking)             |
| x    | H    | H    | Isolate                      |
| PWM  | H    | L    | Rotate (TODO: OUT1 > OUT2 ?) |
| PWM  | L    | H    | Rotate (TODO: OUT1 > OUT2 ?) |

## Connection to Motor 

Out 1 / Out 3 -> Motor +ve Lead

Out 2 / Out 4 -> Motor -ve Lead

## **Physical**

**PCB Size**  55x55x16mm  

**Mounting hole size**  3mm

**Weight** 32g

## Purchase

双路直流电机驱动板模块工业级马达正反转PWM调速L298逻辑7A160W

https://detail.tmall.com/item.htm?id=545415074433&spm=a1z09.2.0.0.32392e8dqyPg5S&_u=jl5jjmhde86 

## PDF

[XY160D_7A_160W_MotorDriver.pdf](XY160D_7A_160W_MotorDriver.pdf) 