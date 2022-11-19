[BAck To Index](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Heart Beat sensor

This sensor uses a bright IR LED (infrared) and a phototransistor to detect the pulse of the finger.
A red LED flashes each pulse.

```c
#include <dummy.h> 
int sensorPin = 36;
double alpha = 0.75;
int period = 100;
double change = 0.0;
double minval = 0.0;
void setup ()
{
  Serial.begin (9600);
}
void loop ()
{
    static double oldValue = 0;
    static double oldChange = 0;
 
    int rawValue = analogRead (sensorPin);
    double value = alpha * oldValue + (1 - alpha) * rawValue;
 
    Serial.print (rawValue);
    Serial.print (",");
    Serial.println (value);
    oldValue = value;
 
    delay (period);
}

```
