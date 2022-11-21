# -
```c
#include <dummy.h>
#include <WiFi.h>
#include <WiFiClientSecure.h>
#include <UniversalTelegramBot.h>


// Wifi network station credentials
#define WIFI_SSID "M32"
#define WIFI_PASSWORD "87654321"
// Telegram BOT Token (Get from Botfather)
#define BOT_TOKEN "5845543294:AAH1XJD5DVVGt4Si8nhUYCzQc9q7vsIFyGo"

const unsigned long BOT_MTBS = 1000; // mean time between scan messages

unsigned long bot_lasttime;          // last time messages' scan has been done

WiFiClientSecure secured_client;
UniversalTelegramBot bot(BOT_TOKEN, secured_client);



void handleNewMessages(int numNewMessages)
{
  Serial.print("handleNewMessages ");
  Serial.println(numNewMessages);
  
  String answer;
  for (int i = 0; i < numNewMessages; i++)
  {
  
    //previously we might used bot.messages[i].text but here to avoid long code every time we made that short as msg.txt
    
    telegramMessage &msg = bot.messages[i];
    Serial.println("Received " + msg.text);
    
    if (msg.text == "/help")
      answer = "So you need _help_, uh? me too! use /start or /status";
      
    else if (msg.text == "/start")
      answer = "Welcome my new friend! You are the first *" + msg.from_name + "* I've ever met";
      
    else if (msg.text == "/status")
      answer = "All is good here, thanks for asking!";
      
    else
      answer = "Say what?";

    bot.sendMessage(msg.chat_id, answer, "Markdown");
  }
}

void bot_setup()
    // Here we Use F-strings: Since we are using command function from the library so to include that while writing that function along with strings.
    //This is used to avoid str.format() in python

{
  const String commands = F("["
                            "{\"command\":\"help\",  \"description\":\"Get bot usage help\"},"
                            "{\"command\":\"start\", \"description\":\"Message sent when you open a chat with a bot\"},"
                            "{\"command\":\"status\",\"description\":\"Answer device current status\"}" // no comma on last command
                            "]");
  bot.setMyCommands(commands);
  //bot.sendMessage("25235518", "Hola amigo!", "Markdown");
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

 bot_setup();

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
