[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# IR Avoidance Sensor
This sensor uses infrared light to detect obstacles. If the emitted infrared light hits an obstacle, it is reflected and detected by the photodiode. The distance that has to be reached for detection can be adjusted with the two controllers one for Distance Change and other ffor sensitivity change.

This sensor also has an enable line. This line can be used to activate or deactivate the detection of the sensor. In the delivery state of the sensor, however, the enable line is deactivated and the sensor is therefore permanently active. If the functionality of the enable line is desired, the jumper EN (green in the picture) must be removed and a corresponding control signal must be applied to the enable pin.

[`Reff link`](https://sensorkit.joy-it.net/en/sensors/ky-032)

| Pins | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Enable`| `Input` | `Digital` |
| `Vcc`| `Input` | `3.3v` |
| `Signal`| `Output` | `Digital` |

| Other Componemts Used on sensor Board|Operation|
| :------------------------- |:------------------------- |
| `Pot1` | `Distance Change`|
| `Pot2`|`Sensitivity Change`|
| `IR transmitter and Reciever`|`-`|

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
