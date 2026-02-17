
# Guide
  ## Objective
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
