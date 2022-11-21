# -

```c
#include <dummy.h>
#include <WiFi.h>
#include <WiFiClientSecure.h>
#include <UniversalTelegramBot.h>


// Wifi network station credentials
#define WIFI_SSID "ssid"
#define WIFI_PASSWORD "password"
// Telegram BOT Token (Get from Botfather)
#define BOT_TOKEN "bottoken"

const unsigned long BOT_MTBS = 1000; // mean time between scan messages

unsigned long bot_lasttime;          // last time messages' scan has been done

WiFiClientSecure secured_client;
UniversalTelegramBot bot(BOT_TOKEN, secured_client);


String test_photo_url = "http://www.thewowstyle.com/wp-content/uploads/2015/01/nature-images.jpg";

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
    //Used String Concatination
      String welcome = "Welcome to Universal Arduino Telegram Bot library, " + from_name + ".\n";
      welcome += "This is Send Image From URL example.\n\n";
      welcome += "/get_test_photo : getting test photo\n";

      bot.sendMessage(chat_id, welcome, "");
    }
  }
}
void setup()
{
  Serial.begin(115200);
  Serial.println();

  // attempt to connect to Wifi network:

  Serial.print("Connecting to Wifi SSID ");
  Serial.print(WIFI_SSID);
  WiFi.begin(WIFI_SSID, WIFI_PASSWORD);
  secured_client.setCACert(TELEGRAM_CERTIFICATE_ROOT); // Add root certificate for api.telegram.org

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
