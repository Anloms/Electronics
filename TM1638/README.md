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
```
void displayValues()
{
        int num[10] = {0x3F, 0x06, 0x5B, 0x4F, 0x66, 0x6D, 0x7D, 0x07, 0x7F, 0x6F};
        int arr[8] = {0, 0, 0, 0, 0, 0, 0, 0};
        int temp = bme.readTemperature();
        int i = 0;
        if (temp == 0)
        {
                arr[0] = 0;
                i = 1;
        }
        else
        {
        while (temp > 0 && i < 8)
        {
                arr[i] = temp % 10;
                temp /= 10;
                i++;
        }
    }
    while (i < 8)
    {
    arr[i] = -1;//b;ank
    i++;
    }
    sendCommand(0x44);
    delayMicroseconds(50);

    sendCommand(0x8F);
    delayMicroseconds(50);

    uint8_t addresses[8] = {0xC0, 0xC2, 0xC4, 0xC6, 0xC8, 0xCA, 0xCC, 0xCE};

    for (int j = 0; j < 8; j++)
    {
        digitalWrite(STB_PIN, LOW);

        shiftOut(DIO_PIN, CLK_PIN, LSBFIRST, addresses[j]);

        if (arr[7-j] >= 0) {
            shiftOut(DIO_PIN, CLK_PIN, LSBFIRST, num[arr[7-j]]);
        } else {
            shiftOut(DIO_PIN, CLK_PIN, LSBFIRST, 0x00);//blank
        }

        digitalWrite(STB_PIN, HIGH);
        delayMicroseconds(50);
        }
}
```  


[Datasheet](https://www.handsontec.com/dataspecs/display/TM1638.pdf)   
[Sending instructions & data - Cheatsheet](TM1638_cheat_sheet.pdf)    
