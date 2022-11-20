[`Back To Index`](https://github.com/Sanjay0302/Sensor-Workshop-#readme)

# Light Cup 

The Light Cup modules contain Mercury Switches that provide a digital signal. The LED's are dimmable.

To use this module you need at least two. (Ofcourse the kit includes 2)

```c
int LedPinA = 34;  //ledpin on sensorboard 
int LedPinB = 35;  //second lebpin of second sensorboard
int ButtonPinA = 25;   //intialize the button for reading the digital value 0 or 1 
int ButtonPinB = 26;   
int buttonStateA = 0;   // intialised state to zero
int buttonStateB = 0;
int brightness = 0;
void setup ()
{
  pinMode (LedPinA, OUTPUT);
  pinMode (LedPinB, OUTPUT);
  pinMode (ButtonPinA, INPUT);
  pinMode (ButtonPinB, INPUT);
}
void loop ()
{
  buttonStateA = digitalRead (ButtonPinA);  // Read 0 or 1
  
  if (buttonStateA == HIGH && brightness! = 255)
  {
    brightness + +;
  }
  
  buttonStateB = digitalRead (ButtonPinB);
  if (buttonStateB == HIGH && brightness! = 0)
  {
    brightness -;
  }
  
  analogWrite (LedPinA, brightness); 
  analogWrite (LedPinB, 255 - brightness);
  delay (25); // 25ms delay
}

```
