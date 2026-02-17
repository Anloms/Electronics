
# Guide

  ## Objective 
  We’ll get hands-on with the BME280 sensor — a cool little device that measures temperature, humidity, and air pressure
  — and the TM1638 controller,  which lets you control LEDs and a built-in display. Along the way, you’ll learn how these components
  talk to each otherand how you can tell them exactly what to do.  

  By the end of this workshop, you’ll have:  
  - Set up a BME280 sensor with an Arduino.
  - Read real data from it.  
  - Tested that data by lighting up an LED.  
  - Wired up a TM1638 controller and display.  
  - Played with its LEDs and display.  
  - Displayed live temperature readings on the TM1638.  
  
  Feeling adventurous? There’s a bonus challenge waiting for you:  
  - Turn the LEDs into a progress bar that fills up as the temperature rises toward a target. It’s a great way to add a little visual flair to your project! 
  
  ## Components we are using   
  
|  | Component | Description | Image | Details |
| :--: | :---: | :---: | :---: | :-----: |
|1 | Arduino | A small, programmable computer (a microcontroller) that reads data from sensors, controls lights and displays, and runs your code. Think of it as the brain of your project. | <img alt="Arduino Nano" src="https://github.com/Anloms/Electronics/blob/main/Arduino_nano.png"/> | [Learn more about Arduino Nano ](#Arduino-Nano) |
|2 | BME280 | A handy sensor module that measures temperature, humidity, and barometric pressure. It’s like a mini weather station on a chip! | <img alt="BME280 temperature, humidity and air pressure sensor" src="https://github.com/Anloms/Electronics/blob/main/BME280_2.png"/> | [Learn more about BME280 ](#BME280) |
|3 | TM1638  | A controller board with 8 LEDs, 8 buttons, and an 8-digit display. It lets you show numbers and control lights, making your project more interactive and visual. | <img alt="TM1638 Control Module" src="https://github.com/Anloms/Electronics/blob/main/TM1638.png"/> | [Learn more about TM1638 ](#TM1638) 
|4 | Jumper Wires - Type A | Usually male-to-male wires used to connect components directly to the Arduino’s pins or a breadboard. Think of them as little bridges for electricity and signals. |<img alt="Various male-to-male, close-to-breadboard Jumper Wires" src="https://github.com/Anloms/Electronics/blob/main/jumper_wires_A.png"/>  | [Learn more about Jumper Wires ](#Jumper-Wires) |
|5 | Jumper Wires - Type B | Often female-to-female or male-to-male wires, great for connecting sensors and modules (like the BME280) to the Arduino without soldering. | <img alt="Various male-to-male Jumper Wires" src="https://github.com/Anloms/Electronics/blob/main/Jumper_wires_B.png"/>   | [Learn more about Jumper Wires ](#Jumper-Wires) |
|6 |  Led Diode  | 		A Light Emitting Diode — a tiny light that lights up when electricity flows through it. It's energy-efficient, colourful, and perfect for visual feedback in your circuits.|<img alt="Various Led Diodes" src="https://github.com/Anloms/Electronics/blob/main/led_diode.png"/>  | [Learn more about Led Diodes ](#Led-Diodes) |
|7 | Resistor  | A component that limits the flow of electricity. It helps control things like LED brightness and protects sensitive parts from getting too much current. | <img alt="Various resistors" src="https://github.com/Anloms/Electronics/blob/main/resistors.png"/> | [Learn more about Resistors ](#Resistors) |
|8 | Raspberry Pi   | A full mini-computer (with an operating system!) that can do everything from running code to browsing the web. In this workshop, it serves as the intermediary between the school's machine and Arduino. |<img alt="Raspberry Pi 3, model B+" src="https://github.com/Anloms/Electronics/blob/main/Pi_3.png"/>  | [Learn more about Raspberry Pi ](#Raspberry-Pi) |  

# Flow part 1 easy & hard with collapsible parts, hints

    
<details>

<summary>Hint</summary>

### Add a header

</details>


  ## Useful utilities and commands:   
  ```bash
  platformio lib install "AM2302-Sensor"
  ```
  ```bash
  rsync -avp oweley@192.168.1.224/temperature_AM2302 --mkpath
  ```
  ```bash
  pio run -t upload --upload-port /dev/ttyUSB0
  ```

  ## LM35DZ Temperature Sensor   

# Troubleshooting
When using Rapbery Pi as an intermediary between Arduino, test whether Ardino is responsive:  
```
PORT="/dev/ttyUSB0" && sudo stty -F $PORT 9600 raw -echo 2>&1 && echo $?
```
If result is `0` then Arduino indeed is responsive.

<br>

# $\LARGE{\textsf{\color{black}{Components - the closer look}}}$   

<br><br>

## $\LARGE{\textsf{\color{black}{Arduino Nano}}}$ 
  The Nano is small — only 45 x 18 mm — which means it fits perfectly on a breadboard right alongside your other components.
  Arduino Nano's brain is ATmega328P Processor, running at 16 MHz . It's reliable, well-supported, and perfect for learning and prototyping.
    
  Memory Specs for Your Code:  
  - 32 KB of flash memory to store your program (like a notebook for your instructions).  
  - 2 KB of SRAM to hold temporary data while running (like a whiteboard for quick notes).  
  - 1 KB of EEPROM to save data even when power is off (like a tiny sticky note that survives a power outage)    
<br><br><br>


## $\LARGE{\textsf{\color{#f5750e}{Pin Breakdown}}}$   

<img alt="Arduino Nano Pinout" src=""/>

<br><br>

### $\LARGE{\text{\color{#326a95}{Digital I/O Pin}}}$
### $\large{\text{\color{#326a95}{These 14 pins are designed to handle binary signals (on or off)}}}$


- ***General Purpose:***  
  You can configure them as INPUT (to read if a button is pressed, 5V or 0V) or OUTPUT (to turn an LED on or off, or control a relay).    
- ***PWM (~Pins 3, 5, 6, 9, 10, 11)***  
      While standard outputs can only be fully ON (5V) or OFF (0V), these specific pins can simulate an analog output using a technique called Pulse-Width Modulation (PWM). 
      They output a square wave that switches on and off so fast that it mimics a voltage between 0 and 5V.    
`Example: This is used to dim LEDs or control the speed of motors.`  

<br>

### $\LARGE{\text{\color{#326a95}{Analog Input Pins (A0-A7)}}}$
### $\large{\text{\color{#326a95}{These pins are designed to read varying voltages from sensors (eg. temperature sensors)}}}$


- ***10-bit ADC:*** They use an Analog-to-Digital Converter. The "10-bit" means they map input voltages between 0 and 5V into integer values between 0 and 1023.  
- ***A6 and A7*** Restriction: On some boards (like the Nano), A6 and A7 are strictly analog input pins. Unlike A0 through A5, they cannot be used as digital input/output pins.  

<br>

### $\LARGE{\text{\color{#326a95}{Power Pins}}}$
### $\large{\text{\color{#326a95}{These pins are used to provide power to the Arduino board itself or to power external components}}}$

- ***VIN (7-12V):*** 
  This is the input voltage pin. If you are using an unregulated power supply (like a battery), you connect the positive lead here. The board has a voltage regulator that converts this down to the 5V needed for operation.  
- ***5V:*** 
  This pin outputs a regulated 5V. It can be used to power 5V sensors. If you are powering the board via USB, this pin will output power. If you supply clean 5V directly to this pin, you can bypass the onboard regulator.   
- ***3.3V:*** 
  This outputs a regulated 3.3V for low-voltage components.   
- ***GND (Ground):*** 
  The common return path for electricity. Having multiple GND pins makes wiring easier, allowing you to keep your circuits tidy.   

<br>

### $\LARGE{\textsf{\color{#326a95}{Specialized Pins}}}$  
### $\large{\textsf{\color{#326a95}{These pins handle specific functions related to the microcontroller's operation}}}$  


***- RST (Reset):*** 
  There are usually two of these. Briefly connecting this pin to GND resets the microcontroller. This restarts your sketch from the beginning. It's useful if your code gets stuck or you want to restart the program without unplugging the power.   
***- AREF (Analog Reference):*** 
  This pin allows you to set a custom maximum voltage for the analog inputs. By default, analogRead() assumes 5V equals a value of 1023. If you connect a voltage (e.g., 2.5V) to the AREF pin and configure the software, the ADC will use that voltage as its reference, providing higher resolution for sensors that output lower voltages.   

 <br><br><br>   
    
   Communication Skills:   
   - I²C — talks to sensors like your BME280 (only needs 2 wires!).   
   - SPI — faster communication for displays and modules.   
   - Serial (UART) — chats with your computer to debug or send data.   
    
   What Can You Build With It?   
   - Sensors & Monitoring - Weather stations, air quality monitors, soil moisture sensors for plants.  
   - Wearables -	Tiny enough to sew into clothing or embed in accessories.  
   - Robotics -	Control small robots, servos, and motors.  
   - Interactive Art	- Light displays, sound-reactive installations, touch-sensitive sculptures.  
   - Automation - Smart home gadgets, automatic plant waterers, pet feeders.  
   
### Useful Links:  
   [More about pins](https://leecuriosity.com/arduino-nano-pinout-full-guide-for-beginners/)  
    
  ## TM1638  
  ## BME280  
  ## Led Diodes  
  ## Resistors  
  ## Jumper Wires  
  ## Raspberry Pi  
