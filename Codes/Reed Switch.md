[Back To Index](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Reed Switch
```c
//This is same as ky024 hall sensor

#define led_builtin 2                  // GPIO 2 is for builtin LED
#include <dummy.h>
int digitalpin = 26;                   // define the Reed sensor interfaces
int analogpin = 36;

void setup ()
{
  pinMode (analogpin , INPUT);
  pinMode (digitalpin, INPUT) ; 
}
void loop ()
{ 
  
  if (digitalRead(digitalpin)== HIGH)   // When the Reed sensor detects a signal, LED flashes
  {
    digitalWrite (led_builtin, HIGH);
  }
  else
  {
    digitalWrite (led_builtin, LOW);
  }

  Serial.print("Analog value");
  Serial.print("   ");
  Serial.println(digitalRead (analogpin));
  
}

```
[Back To Index](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Mini Reed Switch
```c


```
