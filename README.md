
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
  ## Raspberry - Arduino relationship  
  ## Flow 1 - easy & hard with collapsible parts, hints
  ## Flow 2 - easy & hard with collapsible parts, hints 
<details>

<summary>Hint</summary>

### Add a header

</details>


  ## Useful utilities and commands:   
  ```
  platformio lib install "AM2302-Sensor"
  ```
  ```
  rsync -avp oweley@192.168.1.224/temperature_AM2302 --mkpath
  ```
  ```
  pio run -t upload --upload-port /dev/ttyUSB0
  ```

  ## LM35DZ Temperature Sensor   

# Troubleshooting
When using Rapbery Pi as an intermediary between Arduino, test whether Ardino is responsive:  
```
PORT="/dev/ttyUSB0" && sudo stty -F $PORT 9600 raw -echo 2>&1 && echo $?
```
If result is `0` then Arduino indeed is responsive.
