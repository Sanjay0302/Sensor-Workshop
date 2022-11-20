[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# IR Avoidance Sensor
This sensor uses infrared light to detect obstacles. If the emitted infrared light hits an obstacle, it is reflected and detected by the photodiode. The distance that has to be reached for detection can be adjusted with the two controllers one for Distance Change and other ffor sensitivity change.

[`Reff link`](https://sensorkit.joy-it.net/en/sensors/ky-032)

```c
int Led = 2 ;// define onboard LED Interface
int buttonpin = 26; // define the obstacle avoidance sensor interface
int val ;// define numeric variables val
void setup ()
{
  pinMode (Led, OUTPUT) ;// define LED as output interface
  pinMode (buttonpin, INPUT) ;// define the obstacle avoidance sensor output interface
}
void loop ()
{
  val = digitalRead (buttonpin) ;// digital interface will be assigned a value of 26 to read val
  if (val == HIGH) // When the obstacle avoidance sensor detects a signal, LED flashes
  {
    digitalWrite (Led, HIGH);
  }
  else
  {
    digitalWrite (Led, LOW);
  }
}


```
