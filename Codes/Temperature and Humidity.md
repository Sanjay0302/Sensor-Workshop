[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Temprature Sensor ky001
The DS18B20 digital thermometer provides 9-bit to 12-bit Celsius temperature measurements and has an alarm function with non-volatile, user-programmable high and low trigger points.

This means that the sensor has a programmable upper and lower limit. The DS18B20 communicates via a 1-wire bus, which requires only one data line for communication with a central microprocessor. In addition, the DS18B20 can draw power directly from the data line ("parasite power"). This eliminates the need for an external power source.

[`Reff link`](https://sensorkit.joy-it.net/en/sensors/ky-001)
</div>
<div id="header" align="center" >

| Pins | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Gnd`| `Input` | `-` |
| `Vcc`| `Input` | `-` |
| `Signal`| `Output` | `Digital` |

 

</div>

ky001 uses DS18B20 sensor
The DS18B20 sensor has two forms:

- TO-92 package (looks similar to a transistor) Waterproof probe. 
- We use this form in this tutorial.

```c
#include <OneWire.h>
#include <DallasTemperature.h>

#define SENSOR_PIN  21 // ESP32 pin GIOP21 connected to DS18B20 sensor's DQ pin

OneWire oneWire(SENSOR_PIN);
DallasTemperature DS18B20(&oneWire);

float tempC; // temperature in Celsius
float tempF; // temperature in Fahrenheit

void setup() {
  Serial.begin(9600); // initialize serial
  DS18B20.begin();    // initialize the DS18B20 sensor
}

void loop() {
  DS18B20.requestTemperatures();       // send the command to get temperatures
  tempC = DS18B20.getTempCByIndex(0);  // read temperature in °C
  tempF = tempC * 9 / 5 + 32; // convert °C to °F

  Serial.print("Temperature: ");
  Serial.print(tempC);    // print the temperature in °C
  Serial.print("°C");
  Serial.print("  ~  ");  // separator between °C and °F
  Serial.print(tempF);    // print the temperature in °F
  Serial.println("°F");

  delay(500);
}

```

# Analog Temparatur Sensor
This module consist of a NTC thermistor, a 10 kΩ resistor, and 3 male header pins. The thermistor resistance varies according to its surrounding temperature. The value of resistance can be used to calculate the actual temperature.
This module contains a NTC thermistor, which can measure temperatures in the range of -55 °C up to +125 °C. The resistance value decreases at higher temperatures. This has a lower resistance value at higher temperatures. Based on the resulting resistance curve, the corresponding temperature can be calculated.

[`Reff link`](https://sensorkit.joy-it.net/en/sensors/ky-013)

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
 
int sensorPin = 36; // select the input pin 
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
[`Reff link`](https://sensorkit.joy-it.net/en/sensors/ky-028)

This module contains an NTC thermistor, which can measure temperatures in the range of -55°C up to +125°C. The resistance value of the thermistor decreases with increasing temperatures.

This sensor has three functional components on its circuit board: The front sensor unit, which physically measures the environment and outputs it as an analog signal to the second unit, the amplifier. This amplifies the signal depending on the resistance set on the rotary potentiometer and sends it to the analog output of the module.

Here it is to be noted: The signal is inverted. If a high value is measured, this results in a lower voltage value at the analog output.

The third unit represents a comparator, which switches the digital output and the LED when the signal falls below a certain value. This value (and thus the sensitivity of the module) can be adjusted via the rotary potentiometer:

</div>
<div id="header" align="center" >

| Pins | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Gnd`| `Input` | `-` |
| `Vcc`| `Input` | `-` |
| `D0`| `Output` | `Digital` |
| `A0`| `Output` | `Analog` |

</div>

```c
// Declaration and initialization of the input pins
int Analog_Input = 36; // Analog output of the sensor
int Digital_Input = 21; // Digital output of the sensor
  
void setup ()
{
  pinMode (Analog_Input, INPUT);
  pinMode (Digital_Input, INPUT);
       
  Serial.begin (9600); // Serial output with 9600 bps
}
  
// The program reads the current values of the input pins
// and outputs them on the serial output
void loop ()
{
  float Analog;
  int Digital;
    
  //Actual values are read, converted to the voltage value....
  Analog = analogRead (Analog_Input) * (5.0 / 1023.0); 
  Digital = digitalRead (Digital_Input);
    
  //... and output at this position
  Serial.print ("Analog voltage value:"); Serial.print (Analog, 4); Serial.print ("V, ");  //print(Analog,4) prints 4 decimal places
  
  Serial.print ("Limit value:");
  
  if(Digital==1)
  {
      Serial.println (" reached");
  }
  else
  {
      Serial.println (" not yet reached");
  }
  Serial.println ("----------------------------------------------------------------");
  delay (200);
}
```


# Temperature and HumiditySensor

This sensor is a combination of temperature sensor and humidity sensor, united in a compact design. The disadvantage is the low sampling rate of the measurement, so that only every 2 seconds a new measurement result is available. This sensor is therefore particularly suitable for long-term measurements.

	
</div>
<div id="header" align="center" >

| Pins | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Gnd`| `Input` | `-` |
| `Vcc`| `Input` | `-` |
| `Data pin`| `Output` | `Digital` |

| Specificatiom|Description|
| :------------------------- |:------------------------- |
| Sensor Used| DHT11|
 |Measuring range|0 °C to 50 °C|
| Measurement accuracy|	±2 °C|
 |Measurable humidity	|20-90%RH|
 
</div>

[`Reff link1`](https://esp32io.com/tutorials/esp32-temperature-humidity-sensor)
[`Reff link2`](https://sensorkit.joy-it.net/en/sensors/ky-015)

```c

#include <DHT.h>
#define DHT_SENSOR_PIN  21 // ESP32 pin GIOP21 connected to DHT11 sensor
#define DHT_SENSOR_TYPE DHT11

DHT dht_sensor(DHT_SENSOR_PIN, DHT_SENSOR_TYPE);

void setup() {
  Serial.begin(9600);
  dht_sensor.begin(); // initialize the DHT sensor
}

void loop() {
  // read humidity
  float humi  = dht_sensor.readHumidity();
  // read temperature in Celsius
  float tempC = dht_sensor.readTemperature();
  // read temperature in Fahrenheit
  float tempF = dht_sensor.readTemperature(true);

  // check whether the reading is successful or not
  if ( isnan(tempC) || isnan(tempF) || isnan(humi)) {
    Serial.println("Failed to read from DHT sensor!");
  } else {
    Serial.print("Humidity: ");
    Serial.print(humi);
    Serial.print("%");

    Serial.print("  |  ");

    Serial.print("Temperature: ");
    Serial.print(tempC);
    Serial.print("°C  ~  ");
    Serial.print(tempF);
    Serial.println("°F");
  }

  // wait a 2 seconds between readings
  delay(2000);
}

```
