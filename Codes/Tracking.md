[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Tracking Sensor

The sensor module detects whether there is a light-reflecting or light-absorbing surface in front of the sensor. This is output at the digital output of the sensor. This behavior can be used, for example, in controllers such as those used in robots for autonomous line tracking. The sensitivity of the sensor can additionally be adjusted via the two controllers.
[`Reff link`](https://sensorkit.joy-it.net/en/sensors/ky-033)

```c
int Sensor  =  21;  // Declaration of the sensor input spin
   
void setup  ( )
{
  Serial.begin (9600)  ;  // Initialization  serial output
  pinMode (Sensor, INPUT)   ;  //  Initialization Sensorpin
}
  
//  The program reads the current state of the sensor pin and
// displays in the serial console whether the line tracker is currently 
// on the line or not
void loop  ( )
{
  bool val =  digitalRead (sensor)   ;  //  The current signal on the sensor is read
  
  if   (val  = =  HIGH )  //  If a signal has been detected, the LED is switched on.
  {
    Serial.println (“LineTracker is above the line”);
  }
  else
  {
    Serial.println (“Linetracker is out of line”);
  }
  Serial.println (“------------------------------------”)  ;
  delay (500)  ;  // Pasuse between the measurement of 500ms
}
```
