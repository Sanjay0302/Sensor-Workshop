# ESP32 Capacitive Touch Sensor Pins

The ESP32 touch pins can sense variations in anything that holds an electrical charge.
They are often used to wake up the ESP32 from deep sleep.
There are 10 touch GPIO (32,33,27,14,12,13,4,2,15)

# touchRead() Function

```c
// ESP32 Touch Test
// Just test touch pin - Touch0 is T0 which is on GPIO 4.

void setup()
{
  Serial.begin(115200);
  delay(1000); // give me time to bring up serial monitor
  Serial.println("ESP32 Touch Test");
}

void loop()
{
  Serial.println(touchRead(4));  // get value using T0
  //or  Serial.println(touchRead(T0));
  delay(1000);
}

```

# Touch Pins To wake a Esp from Deep Sleep

This code displays how to use deep sleep with
a touch as a wake up source and how to store data in
RTC memory to use it over reboots
`RTC Stands for Real Time Clock`

What is RTC fast memory?
The ESP32 has `16KB of SRAM` called `RTC fast memory` which allows data to be stored even when the processor is put to sleep. 
Data stored in RTC memory is not erased during deep sleep.

The threshold value set here means that when the value read by the touch-sensitive GPIO is below 40, 
the ESP32 should wake up. You can adjust that value accordingly to the desired sensitivity.


```c


#define Threshold 40 //Greater the value, more the sensitivity 

RTC_DATA_ATTR int bootCount = 0;  // boot count saved in RTC memory to hold the data even in deepsleep and use that after a reboot
touch_pad_t touchPin;


void setup(){
  Serial.begin(115200);
  delay(1000);                                                //Take some time to open up the Serial Monitor
  
  ++bootCount;                                                //Increment boot number and print it every reboot
  Serial.println("Boot number: " + String(bootCount));

  //Print the wakeup reason for ESP32 and touchpad too
  print_wakeup_reason();                                      // call user defined function
  print_wakeup_touchpad();                                    // call user defined function
  
  touchAttachInterrupt(T3, callback, Threshold);              // GPIO 15 is T3 touch pin

/*
The callback() function will only be executed if the ESP32 is awake.
If the ESP32 is asleep and you touch T3, the ESP will wake up – the callback() function won’t be executed if you just press and release the touch pin;
If the ESP32 is awake and you touch T3, the callback function will be executed. So, if you want to execute the callback() function when you wake up the ESP32, you need to hold the touch on that pin for a while, until the function is executed.
*/

/*  
If you want to wake up the ESP32 using different touch pins, you just have to attach interrupts to those pins.
Next, you need to use the esp_sleep_enable_touchpad_wakeup() function to set the touch pins as a wake up source.
*/

 
  esp_sleep_enable_touchpad_wakeup();                          //Configure Touchpad as wakeup source (calling inbuilt function)

 
  Serial.println("Going to sleep now");
  esp_deep_sleep_start();                                     //Go to sleep now (calling inbuit function)
  Serial.println("This will never be printed");
}


  //Method to print the reason by which ESP32has been awaken from sleep

void print_wakeup_reason(){
  esp_sleep_wakeup_cause_t wakeup_reason;

  wakeup_reason = esp_sleep_get_wakeup_cause();

  switch(wakeup_reason)
  {
    case ESP_SLEEP_WAKEUP_TOUCHPAD : Serial.println("Wakeup caused by touchpad"); break;
   
//    case ESP_SLEEP_WAKEUP_EXT0 : Serial.println("Wakeup caused by external signal using RTC_IO"); break;
//    case ESP_SLEEP_WAKEUP_EXT1 : Serial.println("Wakeup caused by external signal using RTC_CNTL"); break;
//    case ESP_SLEEP_WAKEUP_TIMER : Serial.println("Wakeup caused by timer"); break;
//    case ESP_SLEEP_WAKEUP_ULP : Serial.println("Wakeup caused by ULP program"); break;
    
    default : Serial.printf("Wakeup was not caused by deep sleep: %d\n",wakeup_reason); break;
  }
}

/*
Method to print the touchpad by which ESP32
has been awaken from sleep
*/
void print_wakeup_touchpad(){
  touchPin = esp_sleep_get_touchpad_wakeup_status();

  switch(touchPin)
  {

      case 3  : Serial.println("Touch detected on GPIO 15"); break;
//    case 0  : Serial.println("Touch detected on GPIO 4"); break;
//    case 1  : Serial.println("Touch detected on GPIO 0"); break;
//    case 2  : Serial.println("Touch detected on GPIO 2"); break;
   
//    case 4  : Serial.println("Touch detected on GPIO 13"); break;
//    case 5  : Serial.println("Touch detected on GPIO 12"); break;
//    case 6  : Serial.println("Touch detected on GPIO 14"); break;
//    case 7  : Serial.println("Touch detected on GPIO 27"); break;
//    case 8  : Serial.println("Touch detected on GPIO 33"); break;
//    case 9  : Serial.println("Touch detected on GPIO 32"); break;
//    default : Serial.println("Wakeup not by touchpad"); break;
  }
}

void callback(){
  //placeholder callback function

}
void loop(){
  //This will never be reached since interrupt method is used not the polling
}

```
