# TM1638   
## Instructions  
```
#define STB_PIN  4
#define CLK_PIN  2
#define DIO_PIN  3
```   
```
        //define pins as outputs
        pinMode(STB_PIN, OUTPUT);
        pinMode(CLK_PIN, OUTPUT);
        pinMode(DIO_PIN, OUTPUT);

        //initial states
        digitalWrite(STB_PIN, HIGH);
        digitalWrite(CLK_PIN, HIGH);
        digitalWrite(DIO_PIN, HIGH);
```  
```
        //Turn display ON (brightness level 4 (C) - medium, level 7 (F) - highest)
        digitalWrite(STB_PIN, LOW);
        shiftOut(DIO_PIN, CLK_PIN, LSBFIRST, 0x8C);
        digitalWrite(STB_PIN, HIGH);
```   
```
        digitalWrite(STB_PIN, LOW);
        shiftOut(DIO_PIN, CLK_PIN, LSBFIRST, 0xC0);
        for (int i =0; i< 16;i++)
        {
                shiftOut(DIO_PIN, CLK_PIN, LSBFIRST, 0x01);
                delay(500);
        }
        digitalWrite(STB_PIN, LOW);
        shiftOut(DIO_PIN, CLK_PIN, LSBFIRST, 0xC0);
        for (int i =0; i< 16;i++)
        {
                shiftOut(DIO_PIN, CLK_PIN, LSBFIRST, 0x00);
                delay(500);
        }
        digitalWrite(STB_PIN, HIGH);
```  


[Datasheet](https://www.handsontec.com/dataspecs/display/TM1638.pdf)   
[Sending instructions & data - Cheatsheet](TM1638_cheat_sheet.pdf)    
