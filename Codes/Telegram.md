# Template

![image](https://user-images.githubusercontent.com/90672297/203082781-cc4198bd-8e74-4513-9b6b-4f318f945586.png)



# Getting updates
There are two mutually exclusive ways of receiving updates for your bot - the getUpdates method on one hand and webhooks on the other. Incoming updates are stored on the server until the bot receives them either way, but they will not be kept longer than 24 hours.

Regardless of which option you choose, you will receive JSON-serialized Update objects as a result.

![image](https://user-images.githubusercontent.com/90672297/203086804-06e9f962-dee6-4a06-af68-b7559660a2a0.png)

[`Available Types`](https://core.telegram.org/bots/api#available-types)
[`Chat Update methods`](https://core.telegram.org/bots/api#chat)
[`Message Update Methods`](https://core.telegram.org/bots/api#message)

Requirements For Below Message Type:

-[`Photo Sending`](https://core.telegram.org/bots/api#photosize)

-[`Document`](https://core.telegram.org/bots/api#document)

-[`Video`](https://core.telegram.org/bots/api#video)

-[`MORE in this documentation`](https://core.telegram.org/bots/api#voice)

```c
#include <dummy.h>
#include <ESP8266WiFi.h>
#include <WiFiClientSecure.h>
#include <UniversalTelegramBot.h>

const unsigned long BOT_MTBS = 1000; // mean time between scan messages

// Wifi network station credentials
#define WIFI_SSID "YOUR_SSID"
#define WIFI_PASSWORD "YOUR_PASSWORD"
// Telegram BOT Token (Get from Botfather)
#define BOT_TOKEN "XXXXXXXXX:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"

unsigned long bot_lasttime;          // last time messages' scan has been done
X509List cert(TELEGRAM_CERTIFICATE_ROOT);
WiFiClientSecure secured_client;
UniversalTelegramBot bot(BOT_TOKEN, secured_client);

void handleNewMessages(int numNewMessages)
{
  for (int i = 0; i < numNewMessages; i++)
  {
    String chat_id = bot.messages[i].chat_id;
    String text = bot.messages[i].text;

    String from_name = bot.messages[i].from_name;
    if (from_name == "")
      from_name = "Guest";

// In the Below if else ladder we write write what should be the replay for recieved
    if (condition)
    {
      
    }
    else if (text == "/start")
    {
      
    }
  }
}

void setup()
{
  Serial.begin(115200);
  Serial.println();

  // attempt to connect to Wifi network:
  configTime(0, 0, "pool.ntp.org");      // get UTC time via NTP
  secured_client.setTrustAnchors(&cert); // Add root certificate for api.telegram.org
  Serial.print("Connecting to Wifi SSID ");
  Serial.print(WIFI_SSID);
  WiFi.begin(WIFI_SSID, WIFI_PASSWORD);
  while (WiFi.status() != WL_CONNECTED)
  {
    Serial.print(".");
    delay(500);
  }
  Serial.print("\nWiFi connected. IP address: ");
  Serial.println(WiFi.localIP());


}

void loop()
{
  //Millis() Reff: https://arduinogetstarted.com/reference/arduino-millis
  
  if (millis() - bot_lasttime > BOT_MTBS)
  {
    int numNewMessages = bot.getUpdates(bot.last_message_received + 1);

    while (numNewMessages)
    {
      Serial.println("got response");
      handleNewMessages(numNewMessages);
      numNewMessages = bot.getUpdates(bot.last_message_received + 1);
    }

    bot_lasttime = millis();
  }
}
```
# Sending Photo Using Url

Replace The `Void handleNewMessages()` function  

```c

String test_photo_url = "PASTE_URL_HERE";

void handleNewMessages(int numNewMessages) {
  Serial.print("handleNewMessages ");  // print on serial MON that's it
  Serial.println(numNewMessages);      //These of int Data type Indicates No. of new msg that are queued 

  for (int i=0; i<numNewMessages; i++) {
    String chat_id = bot.messages[i].chat_id;     //Every new msg will have unique chat_id
    String text = bot.messages[i].text;           //Print the the txt recieved

    String from_name = bot.messages[i].from_name; //Get the Name of the Client
    if (from_name == "") from_name = "Guest";     

    //The Below if else Ladder will decide the Response to the Txt recieved
    
    if (text == "/get_test_photo") {
      bot.sendPhoto(chat_id, test_photo_url, "Caption is optional, you may not use photo caption");
    }

    if (text == "/start") {
      String welcome = "Welcome to Universal Arduino Telegram Bot library, " + from_name + ".\n";
      welcome += "This is Send Image From URL example.\n\n";
      welcome += "/get_test_photo : getting test photo\n";

      bot.sendMessage(chat_id, welcome, "");
    }
  }
}
```
