[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Hall Sensor (Digital)


</div>
<div id="header" align="center" >

| Pins | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Gnd`| `Input` | `-` |
| `Vcc`| `Input` | `-` |
| `Signal`| `Output` | `Digital` |

| Other Componemts Used on sensor Board|
| :------------------------- |
| On board LED |
| Hall Sensor|
| 680 ohms Resistor|

</div>

```c
// refrence video: https://youtu.be/hV8mqPxEAUY\

// ky003 is a digital sensor where output is indicted using 0 and 1 so to read analog values we use ky024
// in ky003 the top side of the sensor is sensitive only to one particular pole that is either north or south pole and the back side will be sensitive to opposite to that of th top side.

#include <dummy.h>            
int sensorpin = 26;           // using digital pin 25 0r 26
int sensorvalue = 0;          //sensor initial value

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
  
```

# Linear Hall Sensor (Analog) 

| Pins | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Gnd`| `Input` | `-` |
| `Vcc`| `Input` | `-` |
| `D0`| `Output` | `Digital` |
| `A0`| `Output` | `Analog` |

| Other Componemts Used on sensor Board | Resistor value |
| :-------------------------  | :-------------------------  |
| On board LED | R1 10k |
| Hall Sensor|  R2 100k |
|Pot | R3 150 |
|LM 393 | R4 1k |
|6 Resistor | R5 1k |
|2 LED | R6 100k |

```c
int Led = 2 ; // define onboard LED Interface
int buttonpin = 36; // define the linear Hall magnetic sensor interface
int val ; // define numeric variables val
void setup ()
{
  pinMode (Led, OUTPUT) ; // define LED as output interface
  pinMode (buttonpin, INPUT) ; // define linear Hall magnetic sensor output interface
}
void loop ()
{
  val = digitalRead (buttonpin) ; // digital interface will be assigned a value of 3 to read val
  if (val == HIGH) // When the linear Hall sensor detects a magnetic signal, LED flashes
  {
    digitalWrite (Led, HIGH);
  }
  else
  {
    digitalWrite (Led, LOW);
  }
}

```
