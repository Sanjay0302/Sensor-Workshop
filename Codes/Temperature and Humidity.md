[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)


# Analog Temparatur Sensor
This module consist of a NTC thermistor, a 10 kΩ resistor, and 3 male header pins. The thermistor resistance varies according to its surrounding temperature. The value of resistance can be used to calculate the actual temperature.

</div>
<div id="header" align="center" >

| Pins | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Gnd`| `Input` | `-` |
| `Vcc`| `Input` | `-` |
| `Signal`| `Output` | `Analog` |

| Sensor Specification|Value|
| :------------------------- | :------------------------- |
| `Operating Voltage`|`5v`|
| `Accuracy`|`±0.5℃`|
| `Temp Range`|`-55 to 125 ℃`|

</div>

```c
#include <math.h>
 
int sensorPin = 36; // select the input pin for the potentiometer
 //RawADC means the ADC value collected from the analog pin where sensor is connected
 
double Thermistor(int RawADC) {
  double Temp;
  Temp = log(10000.0*((1024.0/RawADC-1))); 
  Temp = 1 / (0.001129148 + (0.000234125 + (0.0000000876741 * Temp * Temp ))* Temp );
  Temp = Temp - 273.15;            // Convert Kelvin to Celcius
   //Temp = (Temp * 9.0)/ 5.0 + 32.0; // Convert Celcius to Fahrenheit
   return Temp;
}
 
void setup() {
 Serial.begin(9600);
}
 
void loop() {
 int readVal=analogRead(sensorPin);
 double temp =  Thermistor(readVal);
 
 Serial.println(temp);  // display tempature
 //Serial.println(readVal);  // display tempature
 
 delay(500);
}

```

# Digital Temparatur Sensor
```c

```


# Temperature and HumiditySensor
```c

```
