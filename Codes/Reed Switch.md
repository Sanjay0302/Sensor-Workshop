[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Reed Switch Analog 
A reed switch is a switch that needs a magnet in front of it to switch on or off

Components on sensor board are same as Linear hall sensor

</div>
<div id="header" align="center" >
  
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
</div>

```c
//This is same as ky024 hall sensor

#define led_onboard 2                  // GPIO 2 is for builtin LED
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
    digitalWrite (led_onboard, HIGH);
  }
  else
  {
    digitalWrite (led_onboard, LOW);
  }

  Serial.print("Analog value");
  Serial.print("   ");
  Serial.println(digitalRead (analogpin));
  
}

```


# Mini Reed Switch

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
