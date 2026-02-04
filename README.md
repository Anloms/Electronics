# Electronics

## AM2302 Temperature && humidity sensor   - Success!
  ```
  #include <Arduino.h>
#include <AM2302-Sensor.h>

constexpr unsigned int LED {13};
constexpr unsigned int SENSOR_PIN {2};

AM2302::AM2302_Sensor am2302{SENSOR_PIN};

void setup() {
        Serial.begin(9600);
        pinMode(LED, OUTPUT);
        while (!Serial)
                yield();
        if (am2302.begin())
                delay(3000);
        else
        {
                Serial.print("\n\nErroneus AM2302\n");
                delay(1000);
        }
}

void loop()
{
        static long int prev_temp = 0;
        auto status = am2302.read();
        Serial.print("\n\nStatus: ");
        Serial.println(AM2302::AM2302_Sensor::get_sensorState(status));

        long int temp = am2302.get_Temperature();
        if ((temp == prev_temp) || (prev_temp == 0))
        {
                //Serial.print("\nno temp change: ");
                Serial.print(temp);
                Serial.print("℃ ");
                prev_temp = temp;
        }
        else
        {
                Serial.print("\n\nTemperature has changed from: ");
                Serial.print(prev_temp);
                Serial.print("℃ ");
                Serial.print(" to: ");
                Serial.print(temp);
                Serial.print("℃ ");
                Serial.print("\n\n");
                prev_temp = temp;
                if (temp >= 30)
                {
                        Serial.print("Temperature has reached the threshold!\n");
                        digitalWrite(LED, HIGH);
                }
                else
                {
                        digitalWrite(LED, LOW);
                }

        }
        delay(5000);
}

      
  ```  
  

## LM35DZ Temperature Sensor   

# Troubleshooting
When using Rapbery Pi as an intermediary between Arduino, test whether Ardino is responsive:  
```
PORT="/dev/ttyUSB0" && sudo stty -F $PORT 9600 raw -echo 2>&1 && echo $?
```
If result is `0` then Arduino indeed is responsive.
