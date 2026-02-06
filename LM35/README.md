# LM35 temperature, humidity and altitude sensor   

```
#include <Arduino.h>
#include "LM35IC.h"
using LM35::LM35IC;
constexpr unsigned int LED {13};

const uint8_t pin = A0;
LM35IC sensor = LM35IC(pin);

void setup() {
        Serial.begin(9600);
        pinMode(LED, OUTPUT);
        while (!Serial)
                yield();
}

void loop()
{
        static long int prev_temp = 0;
        double temp = sensor.readTemp();
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
                        Serial.print("Temperature is >= 30 degrees\n");
                        digitalWrite(LED, HIGH);
                }
                else
                {
                        digitalWrite(LED, LOW);
                }

        }
        delay(10000);
}
```    

        
                        digitalWrite(LED, LOW);
                }
```
