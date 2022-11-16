```c
//Program Code

// refrence video: https://youtu.be/hV8mqPxEAUY\

// ky003 is a digital sensor where output is indicted using 0 and 1 so to read analog values we use ky024
// in ky003 the top side of the sensor is sensitive only to one particular pole that is either north or south pole and the back side will be sensitive to opposite to that of th top side.

#include <dummy.h>            
int sensorpin = 26;                         // using digital pin 25 0r 26
int sensorvalue = 0;                        //sensor initial value

void setup()
{
  Serial.begin(9600);
  pinMode(sensorpin, INPUT); 
  
}

void loop()
{
    sensorvalue = digitalRead(sensorpin);   // digital read only 0 or 1
    Serial.println("Sensorvalue: ");        // println means print in next line
    Serial.print(sensorvalue);              // print   means just print in the same line or at the position of the cursor
  
}

```
