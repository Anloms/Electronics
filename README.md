# Electronics
# Troubleshooting
When using Rapbery Pi as an intermediary between Arduino, test whether Ardino is responsive:  
```
PORT="/dev/ttyUSB0" && sudo stty -F $PORT 9600 raw -echo 2>&1 && echo $?
```
If result is `0` then Arduino indeed is responsive.
