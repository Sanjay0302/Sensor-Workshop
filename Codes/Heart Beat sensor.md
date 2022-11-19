[BAck To Index](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Heart Beat sensor

 </div>
<div id="header" align="center" >
 
This sensor uses a bright IR LED (infrared) and a phototransistor to detect the pulse of the finger.
A red LED flashes each pulse.

 | Pins | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `Gnd`| `Input` | `-` |
| `Vcc`| `Input` | `-` |
| `Signal`| `Output` | `Analog` |
 
</div>


 


```c
int Led=13;
int SENSOR=3;
int val;
void setup()
{
pinMode(Led,OUTPUT);
pinMode SENSOR,INPUT);
}
void loop()
{
val=digitalRead(SENSOR);
if(val>=600)
{
digitalWrite(Led, HIGH);
}
Else
{
digitalWrite(Led, LOW);
}
}

```
 
[`Reffrence Link`](https://create.arduino.cc/projecthub/Johan_Ha/from-ky-039-to-heart-rate-0abfca)
