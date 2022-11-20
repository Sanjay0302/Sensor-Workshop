[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Ball Switch

This sensor contains a small metal ball which will complete a circuit depending on the position in the sensor. Because the sensor is very basic, it can only detect large changes when its tilt, and can not measure the angle of its tilt.

```c
int Led = 2 ;// define LED Interface
int buttonpin = 26; // define the tilt switch sensor interfaces
int val ;// define numeric variables val
void setup ()
{
  pinMode (Led, OUTPUT) ;// define LED as output interface
    pinMode (buttonpin, INPUT) ;//define the output interface tilt switch sensor
}
void loop ()
{
  val = digitalRead (buttonpin) ;// digital interface will be assigned a value of 3 to read val
    if (val == HIGH) //When the tilt sensor detects a signal when the switch, LED flashes
  {
    digitalWrite (Led, HIGH);
  }
  else
  {
    digitalWrite (Led, LOW);
  }
}
```
