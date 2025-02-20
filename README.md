# RTC_PCF8563-Tutorial
A tutorial how to use the rtc-pcf8563 with an arduino uno.

Connect your RTC like this to the arduino.
![circuit](https://github.com/user-attachments/assets/a4107417-b71a-4cfa-9e0a-2afb7f46bf3e)

And import this code.
```
#include <Wire.h>
#include "RTClib.h"

RTC_PCF8563 PCF8563;

void setup()
{
  Serial.begin(9600);
  PCF8563.begin();
  PCF8563.adjust(DateTime(2025, 2, 13, 16, 26, 0)); //set to your current time
  delay(2000);
}

void loop()
{
  
  DateTime time = PCF8563.now(); //get the current date and time

  Serial.print(time.year()); //print the current year
  Serial.print(".");
  Serial.print(time.month()); //print the current month
  Serial.print(".");
  Serial.print(time.day());
  Serial.print(" ");
  Serial.print(time.hour());
  Serial.print(":");
  Serial.print(time.minute());
  Serial.print(":");
  Serial.print(time.second());
  Serial.println("");
}
```
Don't forget to install the dependent libraries.

If you do everything correctly this code should work.
