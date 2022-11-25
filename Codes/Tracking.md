[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Tracking Sensor

The sensor module detects whether there is a light-reflecting or light-absorbing surface in front of the sensor. This is output at the digital output of the sensor. This behavior can be used, for example, in controllers such as those used in robots for autonomous line tracking. The sensitivity of the sensor can additionally be adjusted via the two controllers.

![image](https://user-images.githubusercontent.com/90672297/204038459-57cd63ea-c4a8-453a-864c-c756096e52dc.png)


[`Reff link`](https://sensorkit.joy-it.net/en/sensors/ky-033)

| Pins | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Gnd`| `Input` | `-` |
| `Vcc`| `Input` | `-` |
| `Signal`| `Output` | `Digital` |

```c




#define signalpin 21
#define LED_BUILTIN 2

void setup() {
Serial.begin(9600);
pinMode(signalpin,INPUT);
pinMode(LED_BUILTIN, OUTPUT);

}

void loop() 
{
  
  bool value = digitalRead(signalpin);
  if(value == 0)
  {
    digitalWrite(LED_BUILTIN, HIGH);
    Serial.println("LineTracker is out of line");
    Serial.println(value);

  }
  else
  {
     digitalWrite(LED_BUILTIN, LOW);
     Serial.println("LineTracker is above the line");
     Serial.println(value);
  }
  
 delay(500);
  
}
```
