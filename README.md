# RTC_PCF8563-Tutorial
A tutorial how to use the rtc-pcf8563 with an arduino uno.

Connect your RTC like this to the arduino.
![circuit](https://github.com/user-attachments/assets/a4107417-b71a-4cfa-9e0a-2afb7f46bf3e)

And import this code.
```// vychazi z navody.dratek.cz
//using an lcd to show the time and date

#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <DHT.h>
#include "RTClib.h"

bool cbl = false;

LiquidCrystal_I2C lcd(0x27, 16, 2);
DHT dht(5, DHT11);
RTC_PCF8563 PCF8563;

void setup()
{
  lcd.begin();
  dht.begin();
  PCF8563.begin();
  lcd.backlight();
  if(cbl == true) {
    lcd.setCursor ( 0, 0 );
    lcd.print("---CuboidLabs---");
  }
  else{
    lcd.setCursor ( 0, 0 );
    //lcd.print("------Text------");
  }
  PCF8563.adjust(DateTime(2025, 2, 13, 16, 26, 0));
  delay(2000);
}

void loop()
{
  float tep = dht.readTemperature();
  float vlh = dht.readHumidity();
  
  DateTime time = PCF8563.now();

  lcd.setCursor(0,0);
  lcd.print(time.year());
  lcd.setCursor(4,0);
  lcd.print(".");
  lcd.setCursor(5,0);
  lcd.print(time.month());
  lcd.setCursor(7,0);
  lcd.print(".");
  lcd.setCursor(8,0);
  lcd.print(time.day());
  lcd.setCursor(0,1);
  lcd.print(time.hour());
  lcd.setCursor(2,1);
  lcd.print(":");
  lcd.setCursor(3,1);
  lcd.print(time.minute());
  lcd.setCursor(6,1);
  lcd.print(":");
  lcd.setCursor(7,1);
  lcd.print(time.second());
}
```

If you do everything correct this code should work.

PS: if you are not using an lcd_I2C display this code wont work
