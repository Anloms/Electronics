
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
  
  ## Components we are using - to each add picture and details about it  
  
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

  
  ## Raspberry - Arduino relationship  
  ## Flow 1 - easy & hard with collapsible parts, hints
  ## Flow 2 - easy & hard with collapsible parts, hints 
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

# Components - the closer look    
  ## Arduino Nano  
  ## TM1638  
  ## BME280  
  ## Led Diodes  
  ## Resistors  
  ## Jumper Wires  
  ## Raspberry Pi  
