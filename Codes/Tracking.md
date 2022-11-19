[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Tracking Sensor

This sensor can detect lines in black and white. You could for example make a robot/car follow a line.

```c
///Arduino Sample Code
void setup()
{
  Serial.begin(9600);
}
void loop()
{
  Serial.println(digitalRead(26)); // print the data from the sensor
  delay(500);
}

```
