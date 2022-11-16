```c
//Joystick Program Code

//Code write by Moz for YouTube changel LogMaker360, 12-10-2015
//Code belongs to this video: https://www.youtube.com/watch?v=-h_FQR-KcAY

int JoyStick_X = 36; // x //for esp32 use analoog pin number
int JoyStick_Y = 39; // y
int JoyStick_Z = 34; // button
void setup ()
{   
  // Here we select the pin and its mode of operation
  //syntax : pinMode(pin, mode) reff : https://www.arduino.cc/reference/en/language/functions/digital-io/pinmode/
  pinMode (JoyStick_X, INPUT);  
  pinMode (JoyStick_Y, INPUT);
  pinMode (JoyStick_Z, INPUT);                // z is initialised to assign Button in sensor
  
  Serial.begin (9600);                        // 9600 bps baudrate

}
void loop ()
{
  int x, y, z;                                //initialise
  x = analogRead (JoyStick_X);                //read the values from pins continously and assign to variable continously
  y = analogRead (JoyStick_Y);                // analogread() reff : https://randomnerdtutorials.com/esp32-adc-analog-read-arduino-ide/
  z = analogRead (JoyStick_Z);

  // syntax :Serial.print()
  // print only decimal without floating point reff : https://www.arduino.cc/reference/en/language/functions/communication/serial/print/
  
  Serial.print(" X axis = ");                 
  Serial.print (x, DEC);                        
  Serial.print("       Y axis = ");           
  Serial.print (y, DEC);                      
  Serial.print("       Button  value = ");    
  Serial.print (z, DEC);
  delay(100);                                 // delay 0.1sec or 100msec
  if(z == 0){                                 
  Serial.print(" BUTTON is PRESSED");         
  delay(1000);                                
  }                                           
  Serial.println(); // start a new line
  delay (100);
}



```
