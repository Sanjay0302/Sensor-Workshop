[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Temprature Sensor ky001

</div>
<div id="header" align="center" >

| Pins | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Gnd`| `Input` | `-` |
| `Vcc`| `Input` | `-` |
| `Signal`| `Output` | `Analog` |

 

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
[`Reff link`](https://esp32io.com/tutorials/esp32-temperature-humidity-sensor)

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
