# Host mode (Serial Bluetooth)

The first thing we will learn is how to configure our ESP32 in host mode in serial mode to receive and send data. This will allow us to connect from other devices and control the operation of this microcontroller, or simply send data.

To do this, we will use this example in which we activate an LED connected to the microcontroller remotely through the mobile. In my case I had to use an external LED because the card’s LED is connected to the serial pin, and since we are going to use this communication, it does not work correctly.

```c

#include "BluetoothSerial.h" // We will include the Serial Bluetooth header

#if !defined(CONFIG_BT_ENABLED) || !defined(CONFIG_BLUEDROID_ENABLED)
#error Bluetooth is not enabled! Please run `make menuconfig` to and enable it
#endif

#define LED 2
BluetoothSerial BT; // Bluetooth Object

void setup() {
  Serial.begin(9600); // Initializing serial connection for debugging
  BT.begin("ESP32_LED_Control"); // Name of your Bluetooth Device and in slave mode
  Serial.println("Bluetooth Device is Ready to Pair");

  pinMode (LED, OUTPUT); // Change the LED pin to OUTPUT
}

void loop() {
  if (BT.available()) // Check if we receive anything from Bluetooth
  {
    int incoming = BT.read(); // Read what we recevive 
    Serial.print("Received: ");
    Serial.println(incoming);

    if (incoming == 49){ // 1 in ASCII
      digitalWrite(LED, HIGH); // LED On
      BT.println("LED turned ON"); // Send the text via BT Serial
    }

    if (incoming == 48){ // 0 in ASCII
      digitalWrite(LED, LOW); // LED Off
      BT.println("LED turned OFF"); // Send the text via BT Serial
    }
  }
  delay(20);
}

```

![image](https://user-images.githubusercontent.com/90672297/204042480-c28c4c3f-d63e-4dc3-9b1b-57fdc9069e67.png)

