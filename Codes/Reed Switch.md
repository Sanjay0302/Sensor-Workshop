[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Reed Switch
Components on sensor board are same as Linear hall sensor

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
[Back To Index](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Mini Reed Switch
```c


```
