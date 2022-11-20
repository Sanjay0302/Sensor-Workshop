# Shock Sensor

The KY-002 is a shock and vibration sensor. It consists of a conductive outer shell, which closes the contact with an internal spring in case of vibrations and thus emits a signal.
[`Reff link`](https://sensorkit.joy-it.net/en/sensors/ky-002)

```c
//This is a sample program that lights up an LED when a signal is detected at the sensor.

int Led = 2;// declaration of the LED output pin
int Sensor = 21 ;// Declaration of the sensor input pin
int val; // Temporary variable
  
void setup ()
{
  pinMode (Led, OUTPUT) ; // Initialize output pin
  pinMode (Sensor, INPUT) ; // Initialize sensor pin
  digitalWrite(Sensor, HIGH) ; // Activate internal pull-up resistor
}
  
void loop ()
{
  val = digitalRead (Sensor) ; // The current signal at the sensor is read out
  
  if (val == HIGH) // If a signal could be detected, the LED is switched on.
  {
    digitalWrite (Led, LOW);
  }
  else
  {
    digitalWrite (Led, HIGH);
  }
}

```
