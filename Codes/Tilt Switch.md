[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Tilt Switch

The Tilt Switch is a mercury tilt switch that allows you to detect the tilt of your object. It provides a digital output.

</div>
<div id="header" align="center" >

| Pins | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Gnd`| `Input` | `-` |
| `Vcc`| `Input` | `-` |
| `Signal`| `Output` | `Digital` |

| Other Componemts Used on sensor Board|
| :------------------------- |
| `Res - 10k and 680 ohms`|
| `Uses Mercury fluid` |

</div>


```c
//KY017 Mercury open optical module
int Led = 2 ;// define onboard LED Interface
int sensorpin = 3; // define the mercury tilt switch sensor interface
int val ;// define numeric variables val
void setup ()
{
  pinMode (Led, OUTPUT) ;// define LED as output interface
  pinMode (sensorpin, INPUT) ;// define the mercury tilt switch sensor output interface
}
void loop ()
{
  val = digitalRead (sensorpin) ;// read the values assigned to the digital interface 3 val
  if (val == HIGH) // When the mercury tilt switch sensor detects a signal, LED flashes
  {
    digitalWrite (Led, HIGH);
  }
  else
  {
    digitalWrite (Led, LOW);
  }
}


```
