
# $\Huge{\textsf{\color{black}{Guide}}}$  

<br>

 # $\large{\textsf{\color{black}{Objective}}}$  
 <br>
  
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

  <br>
  
  # $\large{\textsf{\color{black}{Components - list}}}$    

  <br><br>
  
|  | Component | Description | Image | Details |
| :--: | :---: | :---: | :---: | :-----: |
|1 | Arduino | A small, programmable computer (a microcontroller) that reads data from sensors, controls lights and displays, and runs your code. Think of it as the brain of your project. | <img alt="Arduino Nano" src="https://github.com/Anloms/Electronics/blob/main/Arduino_nano.png"/> | [Learn more about Arduino Nano ](#arduino-nano) |
|2 | BME280 | A handy sensor module that measures temperature, humidity, and barometric pressure. It’s like a mini weather station on a chip! | <img alt="BME280 temperature, humidity and air pressure sensor" src="https://github.com/Anloms/Electronics/blob/main/BME280_2.png"/> | [Learn more about BME280 ](#bme280) |
|3 | TM1638  | A controller board with 8 LEDs, 8 buttons, and an 8-digit display. It lets you show numbers and control lights, making your project more interactive and visual. | <img alt="TM1638 Control Module" src="https://github.com/Anloms/Electronics/blob/main/TM1638.png"/> | [Learn more about TM1638 ](#tm1638) 
|4 | Jumper Wires - Type A | Usually male-to-male wires used to connect components directly to the Arduino’s pins or a breadboard. Think of them as little bridges for electricity and signals. |<img alt="Various male-to-male, close-to-breadboard Jumper Wires" src="https://github.com/Anloms/Electronics/blob/main/jumper_wires_A.png"/>  | [Learn more about Jumper Wires ](#jumper) |
|5 | Jumper Wires - Type B | Often female-to-female or male-to-male wires, great for connecting sensors and modules (like the BME280) to the Arduino without soldering. | <img alt="Various male-to-male Jumper Wires" src="https://github.com/Anloms/Electronics/blob/main/Jumper_wires_B.png"/>   | [Learn more about Jumper Wires ](#jumper) |
|6 |  Led Diode  | 		A Light Emitting Diode — a tiny light that lights up when electricity flows through it. It's energy-efficient, colourful, and perfect for visual feedback in your circuits.|<img alt="Various Led Diodes" src="https://github.com/Anloms/Electronics/blob/main/led_diode.png"/>  | [Learn more about Led Diodes ](#led-diodes) |
|7 | Resistor  | A component that limits the flow of electricity. It helps control things like LED brightness and protects sensitive parts from getting too much current. | <img alt="Various resistors" src="https://github.com/Anloms/Electronics/blob/main/resistors.png"/> | [Learn more about Resistors ](#resistors) |
|8 | Raspberry Pi   | A full mini-computer (with an operating system!) that can do everything from running code to browsing the web. In this workshop, it serves as the intermediary between the school's machine and Arduino. |<img alt="Raspberry Pi 3, model B+" src="https://github.com/Anloms/Electronics/blob/main/Pi_3.png"/>  | [Learn more about Raspberry Pi ](#raspberry-pi) |  
|9 | Breadboard | A breadboard is a reusable platform for building and testing electronic circuits without soldering. Think of it as a prototyping playground where components can be easily plugged in, moved around, and reused. | <img alt="Breadboard" src="https://github.com/Anloms/Electronics/blob/main/Resources/breadboard_2.png"/> | [Learn more about Breadboards](#breadboard) |

<br><br>

# $\large{\textsf{\color{black}{Flow - Part 1}}}$    

<br><br>

### $\Large{\textbf{\color{#f48522}{1. Setting Up Your Breadboard and Arduino }}}$ 
   Before we connect any fancy sensors, we need to give our Arduino a stable home on the breadboard and provide it with power.   
   - Gently place your Arduino Uno board onto the breadboard so it straddles the center gap. Place it at the very top to leave plenty of room below for your circuit. The USB port should hang slightly over the edge.   

  > [!TIP]
  > Make sure no pins are bent underneath and that the board is seated firmly but gently.   
<br>

### $\Large{\textbf{\color{#f48522}{2. Provide power to the breadboard}}}$   
  The Arduino has pins that can provide power, but we need to connect them to the breadboard's power rails (the long rows of holes marked with red and blue lines on the side).
  - Take a red male-to-male jumper wire. Connect one end to the 5V pin on the Arduino. Connect the other end to a hole in the red (positive) rail on your breadboard.  
  - Take a black (or blue) male-to-male jumper wire. Connect one end to a GND (ground) pin on the Arduino. Connect the other end to a hole in the blue (negative) rail on your breadboard.  

> [!NOTE]
> Why this matters: Now, any component that needs power can draw it from these rails, keeping your circuit organized.    
<br>

### $\Large{\textbf{\color{#f48522}{3. Connecting the BME280 Sensor}}}$  
  Now for the star of the show. We'll connect the sensor using a communication method called I2C, which only uses two wires.   
        
   > [!Important]
   > [Click me to see BME280 data](#BME280)  or [me to see Arduino Nano Pin-out](#Arduino-Nano)  
   <br>
   
  - Identify the Pins: Look at your BME280 sensor. You'll need to identify four pins: 
      - VIN (or VCC),
      - GND
      - SCL (Serial Clock)
      - and SDA (Serial Data)  
  - Make the Connections:  
      - Power (VIN): Use a jumper wire to connect the VIN pin on the sensor to the red (+) power rail on your breadboard.  
      - Ground (GND): Use a jumper wire to connect the GND pin on the sensor to the blue (-) ground rail on your breadboard.  
      - I2C Data (SDA): Use a jumper wire to connect the SDA pin on the sensor to the A4 pin on the Arduino Uno. (On an Uno, A4 is the hardware pin for I2C data).  
      - I2C Clock (SCL): Use a jumper wire to connect the SCL pin on the sensor to the A5 pin on the Arduino Uno. (On an Uno, A5 is the hardware pin for the I2C clock). 
 <br>

### $\Large{\textbf{\color{#f48522}{4. The Software - Reading the Sensor}}}$     
With the hardware connected, let's program the Arduino to talk to the sensor and show us what it sees.  
> [!IMPORTANT]
> Arduino code, including the code we write in PlatformIO, is structured around a simple but powerful execution model using two mandatory functions.
>
> - void setup(): This function is called once when the microcontroller starts or resets. It's designed for one-time initializations. 
>You place code here to configure pin modes (like setting our LED pin as an OUTPUT), initialize serial communication (Serial.begin), and verify that your sensor
>is connected and responding (bme.begin()). It ensures the system is in a known state before beginning its main task.
>
> - void loop() : After setup() finishes, the loop() function is called repeatedly. As the name suggests, it runs in an infinite loop. This is where the main logic of your program resides—reading sensor values, >making decisions (like our if statement for the LED), and updating outputs. This structure is perfect for embedded systems that need to continuously monitor and react to their environment.

<br>

  Install the Required Libraries. Open the Arduino IDE on your computer. Go to Sketch > Include Library > Manage Libraries... In the Library Manager, search for "Adafruit BME280".
  When prompted, also install any dependencies, especially "Adafruit Unified Sensor".  
  
  
> [!NOTE]
> Why we need it: These libraries contain all the specific commands needed to communicate with the BME280, so we don't have to write them from scratch.  

<br>

# $\large{\textbf{\color{black}{Choose the difficulty level:}}}$   
<br>
<br>
<details><summary> 
 
## $\large{\textsf{\color{#D1242F}{    Guide to writing the software yourself}}}$ 
</summary>

Before we write a single line of code, let's understand what's happening behind the scenes when we want to read from the BME280 sensor.  

How do we communicate?   
The BME280 communicates using I2C (Inter-Integrated Circuit). Think of I2C like a telephone party line:   
- SDA (Serial Data Line) is the conversation itself    
- SCL (Serial Clock) keeps everyone talking in rhythm   
Each device has a unique address so the Arduino knows who it's talking to.   

Step 1: Including Libraries     
```
#include <Wire.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_BME280.h>
```   
<details><summary>:bulb:Libraries Q&A</summary>
<br>
 
 <details><summary>:bulb:Why do we need `Wire.h`? </summary>
<br> 
  
> [!]
>
>  This is Arduino's built-in I2C library. It's like learning the alphabet before writing a letter. Without Wire.h, your Arduino wouldn't know how to:
>  - Start and stop communication on the I2C bus
>  - Send bytes of data
>  - Request data from sensors
>  - Handle the timing of the clock signal 
>
 </details>
  <details>
   <summary>:bulb:What does Wire.h do?</summary>
<br>
   
> [!]
>
>   Wire.h translates your commands into electrical signals on the SDA and SCL pins.
> 

  </details>
    <details>
   <summary>:bulb:Why do we need Adafruit_Sensor.h? </summary>
<br>   
     
> [!]
>
>  This is an interface library. Think of it as a universal translator. It ensures that all sensors (BME280, humidity sensors, motion sensors, etc.) speak a similar language. It provides:  
>  - Standardized ways to get sensor data   
>  - Consistent data structures (like sensor_t for sensor info)   
>  - Common methods like getEvent() across different sensors  
> 

    </details>
    <details>
   <summary>:bulb: Why do we need Adafruit_BME280.h? </summary>
<br>

> [!]
>
>  This is the BME280's personal interpreter. It knows:  
>  - The exact I2C commands the BME280 understands   
>  - How to request temperature vs. humidity vs. pressure   
>  - How to convert the raw bits from the sensor into actual Celsius degrees   
>  - The sensor's specific register addresses (where data is stored)   
>
> Without it, you'd need to read the BME280's 78-page datasheet and manually send register commands! 
>
>

  </details>
</details>

 
Step 2: Creating the Sensor Object   
```
Adafruit_BME280 bme;
```

This line doesn't communicate with the sensor yet. It's like buying a phone and putting it on your desk. The phone exists (the object is created), but it's not connected to a line yet. The object bme now has "methods" (functions) we can use later, like:  
 - bme.begin() - Connect to the actual sensor  
 - bme.readTemperature() - Get temperature reading  
 - bme.readHumidity() - Get humidity reading  
    
Step 3: Macros - Why Use #define?   
```
#define BME_PIN 13
```
<details><summary>:bulb:Macros Q&A</summary>
 <br>
 
<details><summary>:bulb:What is a Macro?</summary>
 <br>

 > [!]
 >
 >A macro is a find-and-replace that happens before your code compiles. Everywhere you write BME_PIN, the compiler replaces it with 13. 
 >
 >
 
</details>
 <details><summary>:bulb:Why Use Macros Instead of Variables?</summary> 
  <br>

> [!]
>
>
> 
> ```
>  // Using a variable:
>  int bme_pin = 13;  // Takes up memory
>  // Using a macro:
>  #define BME_PIN 13  // No memory used! 
>```  
>
>Key benefits:  
>- Zero memory usage - The value is inserted directly into the code   
>- Cannot be accidentally changed - It's not a variable, so no code can modify it    
>- Better documentation - The name explains what the number means   
>- Easy updates - Change it once, and it updates everywhere   
>
>
>

 </details>
 
</details>

Step 4: The setup() Function   

```
void setup() {
  Serial.begin(9600);
  
  if (!bme.begin(0x76)) {
    Serial.println("Sensor not found!");
    while (1);
  }
}
```  

<details><summary> :bulb: setup() Q&A</summary>
<br>
 
<details><summary>:bulb:Why Serial.begin(9600)?  </summary>
<br>
 
> [!]
> 
>  This opens a communication channel between your Arduino and computer. Think of it as opening a walkie-talkie channel:  
>  - Serial - The walkie-talkie itself   
>  - begin(9600) - Tuning to channel "9600" (baud rate)  
>9600 means 9600 bits per second. It's like agreeing to talk at a certain speed so you can understand each other. Both devices must use the same speed!  
>
>

</details>
 <details><summary>:bulb: What is happening behind bme.begin(0x76)</summary>
<br>  
  
> [!]
>  
> This is where the actual conversation with the sensor begins:   
>```
>if (!bme.begin(0x76)) {
>```  
>This line does so much behind the scenes:  
>- Activates the I2C bus through Wire.h  
>- Sends a "ping" to address 0x76 to see if anything responds   
>- Reads the chip ID from the sensor to confirm it's really a BME280  
>- Reads calibration data from the sensor's memory   
>- Configures the sensor's default settings (sampling rates, filter, etc.)   
>
>

 </details>
 <details><summary>:bulb:Why 0x76?</summary>
 <br>
  
 > [!]
 >  Most BME280 boards use address 0x76.  
 > 
 
 </details>
 <details><summary>:bulb:The meaning of !</summary>
 <br>
  
> [!]
> The ! means "if NOT successful". If the sensor doesn't respond, we print an error and stop with while(1) (infinite loop).
>

 </details>
</details>

Step 5: Available Functions - Your Toolkit
Once bme.begin() succeeds, you have access to these main functions:
Temperature Functions:  
```
float tempC = bme.readTemperature();      // Returns Celsius (default)
```     
What happens inside?   
- Sensor measures voltage across its temperature-sensitive element  
- Converts analog reading to digital bits  
- Arduino requests these raw bits via I2C  
- Library applies calibration formulas from the sensor  
- Returns a nice float value in Celsius  

Step 6: The loop() Function - Continuous Monitoring  
```
void loop() {
  float temperature = bme.readTemperature();
  
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" °C");
  
  delay(1000);  // Wait 1 second
}
```   
<details><summary>:bulb: loop Q&A</summary>
<br>
 
<details><summary>:bulb:Why Store in a Variable?  </summary>
<br>
 
> [!]
>
> ```
> float temperature = bme.readTemperature();
> ```
> This stores the reading so you can use it multiple times without re-requesting it from the sensor. If you called bme.readTemperature() three times, you'd get three slightly different readings!
>
>
</details>
<details><summary>:moneybag: Why the delay() is crucial</summary>
<br>
 
> [!]
>
> Without delay(1000), the Arduino would read the sensor millions of times per second, flooding the I2C bus and filling your serial monitor instantly.  
>

</details>
</details>
<br>

****************************************************************
****************************************************************
</details>
<br>


<details><summary> 
 
## $\large{\textsf{\color{#54aeff}{    Just copy the code}}}$
</summary>
 
### $\large{\textsf{\color{black}{BME280 code}}}$  

```   
#include <Wire.h>
#include <SPI.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_BME280.h>

#define BME_SCK 13

Adafruit_BME280 bme; // I2C

void setup()
{
        Serial.begin(9600);
        Serial.println(F("BME280 test"));
        bool status;
        
        status = bme.begin(0x76);
        if (!status)
        {
                Serial.println("Could not find a valid BME280 sensor, check wiring!");
        while (1);
        }

}

void printValues()
{
        Serial.print("Temperature = ");
        Serial.print(bme.readTemperature());
        Serial.println(" *C");

        Serial.println();
        delay(5000);
}

void loop()
{
        printValues();
}
```   

****************************************************************
****************************************************************
</details>
<br>
<img alt="choose wisely" src="https://github.com/Anloms/Electronics/blob/main/Resources/choose_wisely.png"/>  
<br>
<br>

# $\large{\textsf{\color{black}{CLI commands}}}$  

<br>

- Push the code located on the local machine to Raspberry Pi:  
```
  rsync -avp oweley@192.168.1.224/temperature --mkpath
```   
- Search for available Arduino libraries:  
```
  platformio lib search "keyword"
```   
- Install the lib of your choice:  
```
  platformio lib install "Adafruit BME280 Sensor"
```   
- Upload the code from Raspberry Pi to Arduino:  
```
  pio run -t upload --upload-port /dev/ttyUSB0
```  

***

<br>

 

# $\large{\textsf{\color{black}{Components - the closer look}}}$   

<br><br>
<details>
  <summary id="arduino-nano">$\LARGE{\textsf{\color{black}{Arduino Nano}}}$</summary>
 <br><br>
 
 # $\Large{\textbf{\color{#f48522}{Arduino Nano}}}$
 
  Arduino Nano is small — only 45 x 18 mm — which means it fits perfectly on a breadboard right alongside your other components.
  Arduino Nano's brain is ATmega328P Processor, running at 16 MHz . It's reliable, well-supported, and perfect for learning and prototyping.
    
<br><br><br>

### $\Large{\textbf{\color{#f48522}{Pin Breakdown}}}$

<img alt="Arduino Nano Pinout" src="https://github.com/Anloms/Electronics/blob/main/Resources/Nano_pinout.png"/>

<br>

| left side |  |  | right side |  |  |
| :---: | :---: | :---: | :---: | :---: | :---: |
| Physical Pin | General Purpose pin |  Notes | Physical Pin | General Purpose pin | Notes |
| 1 | D13 | Digital I/O, Built-in LED | 30 | D12 | Digital I/O, SPI (MISO) |
| 2 | 3V3 |  Power Output | 29 | D11 | Digital I/O, PWM, SPI (MOSI) |
| 3 | AREF | Analog Reference | 28 | D10 | Digital I/O, PWM, SPI (SS) |
| 4 | A0/D14 | Analog Input or Digital I/O | 27 | D9 | Digital I/O, PWM |
| 5 | A1/D15 | Analog Input or Digital I/O | 26 | D8 | 	Digital I/O |
| 6 | A2/D16 | Analog Input or Digital I/O | 25 | D7 | Digital I/O |
| 7 | A3/D17 | Analog Input or Digital I/O | 24 | D6 | Digital I/O, PWM |
| 8 | A4/D18 | Analog Input or Digital I/O, I2C (SDA) | 23 | D5 | Digital I/O, PWM |
| 9 | A5/D19 | Analog Input or Digital I/O, I2C (SCL) | 22 | D4 | Digital I/O |
| 10 | A6/D20 | Analog Input or Digital I/O | 21 | D3 | Digital I/O, PWM |
| 11 | A7/D21 | Analog Input or Digital I/O | 20 | D2 | Digital I/O |
| 12 | +5V | Power Output/Input | 19 | GND | Power Ground |
| 13 | RST | Reset | 18 | RST | Reset |
| 14 | GND | Power Ground | 17 | D0 / TX | Digital I/O, Serial Transmit |
| 15 | VIN | Power Input | 16 | D0 / RX | Digital I/O, Serial Receive |

<br>

  ### $\Large{\textsf{\color{#326a95}{Dital I/O Pin (0-13)}}}$
  ### $\large{\textsf{\color{#326a95}{These 14 pins are designed to handle binary signals (on or off)}}}$


  - ***General Purpose:***  
    You can configure them as INPUT (to read if a button is pressed, 5V or 0V) or OUTPUT (to turn an LED on or off, or control a relay).    
  - ***PWM (~Pins 3, 5, 6, 9, 10, 11)***  
        While standard outputs can only be fully ON (5V) or OFF (0V), these specific pins can simulate an analog output using a technique called Pulse-Width Modulation (PWM). 
        They output a square wave that switches on and off so fast that it mimics a voltage between 0 and 5V.    
  `Example: This is used to dim LEDs or control the speed of motors.`  

<br>

  ### $\Large{\textsf{\color{#326a95}{Analog Input Pins (A0-A7)}}}$ 
  ### $\large{\text{\color{#326a95}{These pins are designed to read varying voltages from sensors (eg. temperature sensors)}}}$


  - ***10-bit ADC:*** They use an Analog-to-Digital Converter. The "10-bit" means they map input voltages between 0 and 5V into integer values between 0 and 1023.  
  - ***A6 and A7*** Restriction: On some boards (like the Nano), A6 and A7 are strictly analog input pins. Unlike A0 through A5, they cannot be used as digital input/output pins.  

<br>
 
  ### $\Large{\textsf{\color{#326a95}{Power Pins}}}$ 
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

  ### $\Large{\textsf{\color{#326a95}{Specialized Pins}}}$  
  ### $\large{\textsf{\color{#326a95}{These pins handle specific functions related to the microcontroller's operation}}}$  


  - ***RST (Reset):*** 
    There are usually two of these. Briefly connecting this pin to GND resets the microcontroller. This restarts your sketch from the beginning. It's useful if your code gets stuck or you want to restart the   program without unplugging the power.   
  - ***AREF (Analog Reference):*** 
    This pin allows you to set a custom maximum voltage for the analog inputs. By default, analogRead() assumes 5V equals a value of 1023. If you connect a voltage (e.g., 2.5V) to the AREF pin and configure the software, the ADC will use that voltage as its reference, providing higher resolution for sensors that output lower voltages.   

 <br><br><br>   
    
  ### $\Large{\textsf{\color{black}{Communication Skills}}}$  
   - I²C — talks to sensors like your BME280 (only needs 2 wires!).   
   - SPI — faster communication for displays and modules.   
   - Serial (UART) — chats with your computer to debug or send data.   

  ### $\Large{\textsf{\color{black}{Useful links}}}$  
  - [More about pins](https://leecuriosity.com/arduino-nano-pinout-full-guide-for-beginners/)  

<br>

****************

</details>
<details>
 <summary id="tm1638">$\LARGE{\textsf{\color{black}{TM1638}}}$</summary> <br><br>
 
 ## $\Large{\textsf{\color{black}{TM1638}}}$

 *************
 
</details>

<details>
 <summary id="bme280">$\LARGE{\textsf{\color{black}{BME280}}}$</summary><br><br>

 # $\Large{\textbf{\color{#f48522}{BME280}}}$

<img alt="BME280 pinout" src="https://github.com/Anloms/Electronics/blob/main/Resources/BME280_pinout.png">

The BME280 is a combined environmental sensor that measures temperature, humidity, and barometric pressure all in one compact package.
It's manufactured by Bosch Sensortec and is widely used in weather stations, indoor navigation, home automation, and IoT projects.

## $\Large{\textsf{\color{#326a95}{Specs}}}$  
<br>

| Parameter | Range | Accuracy |
| :---: | :---: | :---: |
| Temperature | -40°C to +85°C | ±1.0°C |
| Humidity | 0 - 100% | ±3% |
| Pressure | 300 - 1100 hPa | ±1 hPa |

<br>

## $\Large{\textsf{\color{#326a95}{Pinout Description}}}$ 
<br>

| Pin | Name | Function |
| :---: | :---: | :---: |
| VCC | Power | Connect to 3.3V or 5V |
| GND | Ground | Connect to common ground |
| SCL | Serial Clock | I²C clock line - Carries the data back & forth |
| SDA | Serial Data | I²C data line - Keeps everyone in sync |

<br>

> [!NOTE] I2C Communication Protocol  
>
> I2C (Inter-Integrated Circuit) is a serial communication protocol that allows multiple devices to talk to each other using just two wires.
> It's the standard way to connect sensors, displays, and memory chips to microcontrollers like Arduino.
>
>
> How It Works:  
> Every device on an I2C bus has a unique address (like 0x76 for the BME280). The Arduino (called the controller) initiates all communication:
> - Start: Arduino pulls SDA low while SCL is high → "Everyone listen up!"
> - Address: Arduino sends the address of the device it wants to talk to
> - Acknowledge: The matching device responds → "I'm here!"
> - Data: Information is exchanged in 8-bit chunks
> - Stop: Arduino releases the bus → "Conversation over"
>

<br>

## $\Large{\textsf{\color{#326a95}{Why is it so popular?}}}$
<br>
One of the BME280's strengths is its low power consumption:
    - 3.6 μA at 1Hz sampling rate (humidity, pressure, temperature).  
    - 0.1 μA in sleep mode.   

This makes it ideal for battery-powered projects.

<br>

## $\Large{\textsf{\color{#326a95}{Applications}}}$   
- Weather stations: Monitor environmental conditions  
- Altitude tracking: Pressure changes with elevation   
- Indoor navigation: Detect floor changes in buildings  
- GPS enhancement: Improve positioning accuracy  
- Home automation: HVAC control  

<br>

******************

<br>
</details>

<details>
 <summary id="breadboard">$\LARGE{\textsf{\color{black}{Breadboard}}}$</summary><br><br>

# $\Large{\textbf{\color{#f48522}{Breadboard}}}$  

<br>

A breadboard is a reusable prototyping tool that lets you build electronic circuits without soldering. Think of it as a construction site for circuits — you can plug components in, move them around, and reuse everything when you're done.

<br>

## $\Large{\textsf{\color{#326a95}{The Anatomy of a Breadboard}}}$

1. Holes (Tie Points)  
Those hundreds of tiny holes are where you insert component legs and jumper wires. Each hole is connected to others underneath in a specific pattern.

2. The Hidden Metal Strips
Beneath the plastic, there are metal clips connecting rows of holes. This is the most important thing to understand—the holes aren't all connected randomly!

3. The Center Gap
That groove running down the middle separates the two sides. Chips (like Arduino chips or sensors) straddle this gap so each pin connects to a different row.

4. Power Rails
The long columns marked with red (+) and blue (-) lines run the entire length of the breadboard. These are for power distribution—one connects to 5V, the other to ground.

<br>

## $\Large{\textsf{\color{#326a95}{What is the origin of the name?}}}$  

<br>

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/HrG98HJ3Z6w/0.jpg)](https://www.youtube.com/watch?v=HrG98HJ3Z6w)

<br>

 ***
 
</details>

<details>
 <summary  id="led-diodes">$\LARGE{\textsf{\color{black}{Led Diodes}}}$</summary><br><br>
 
 # Led Diodes

 ***
 
</details>

<details>
 <summary id="resistors">$\LARGE{\textsf{\color{black}{Resistors}}}$</summary><br><br>
 
 # Resistors

 ***
 
</details>

<details>
 <summary id="jumper">$\LARGE{\textsf{\color{black}{Jumper Wires}}}$</summary><br><br>

 # Jumper Wires

 ***
 
</details>

<details>
 <summary id="raspberry-pi"> $\LARGE{\textsf{\color{black}{Raspberry Pi}}}$</summary><br><br>

 # Raspberry Pi

 ***

 
</details>

<br>
<br>

# $\large{\textsf{\color{black}{Troubleshooting}}}$ 
<br>

When using Rapbery Pi as an intermediary between Arduino, test whether Ardino is responsive:  
```
PORT="/dev/ttyUSB0" && sudo stty -F $PORT 9600 raw -echo 2>&1 && echo $?
```
If result is `0` then Arduino indeed is responsive.

<br>

***
