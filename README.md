#  esp8266-wifi-HID
wifi enabled HID device that can be used for executing ducky sripts like the usb rubber ducky
sends payloads from esp8266 to arduino or any device using the ATMEGA32u4


### Preparation

What you will need:
- **ESP8266 Wi-Fi chip**  
  I recommend using an ESP-12. It's widely used, cheap, tiny and has 4MB of flash memory.  
  However if you're a beginner you should probably start with a developer board like the NodeMCU or a Wemos d1 mini.  
- **ATmega32u4**  
  The Arduino Micro and Arduino Leonardo use an ATmega32u4 for example. You could also get a Arduino Pro Micro or other cheap Arduino clones which use the ATmega32u4. I will use an [ATmega32u4 CJMCU Beetle](https://www.google.de/search?q=Cjmcu-beetle&tbm=isch).  
- **(a 3.3V regulator)**  
  I put that in brackets because you will only need this if your ATMega32u4 board doesn't provide 3.3V. The ESP8266 only works with 3.3V, so depending on your board you may need a regulator to get 3.3V out of the 5V.  
- **Some skill, knowledge and common sense on this topic**  
  That's probably the most important part here. **This project is not noob friendly!** If you are a beginner, please start with other projects and get some knowledge about how Arduino and its code works, how to handle errors and how to work with the ESP8266. **I can't cover every little detail here. Please respect that.** Depending on your hardware choices you may need to add or change a bit of the Arduino code.  

So make your hardware choices!  
Also I wouldn't go straight forward and solder everything together. Test it beforehand, otherwise debugging can be hard!

**For an easy start, better debugging, further development or if you just wanna test this project, I recommend using a Nodemcu + an Arduino Leonardo:**
![nodemcu with a leonardo as wifi duck](https://raw.githubusercontent.com/spacehuhn/wifi_ducky/master/images/leonardo_duck_1.jpg)
This is easy to setup, you don't need any soldering skills and you can still use both the NodeMCU and the Arduino for other cool projects.


But now let's get started!  

### ESP8266

First you will need to flash your ESP8266.  
You can either flash the bin file directly or compile it yourself using Arduino.  

**Note:** You will only need to flash it once, every new update can then be done over the possibilities.

If don't use a USB dev board and don't know how to flash your plain ESP8266, I recommend you to have a look at this instructable: http://www.instructables.com/id/Getting-Started-with-the-ESP8266-ESP-12/?ALLSTEPS

You could also use your Arduino to flash it: https://gist.github.com/spacehuhn/b2b7d897550bc07b26da8464fa7f4b36
(The connections are the same for this project, the only difference is that you need to set GPIO-0 to LOW to enabling a firmware update).

**Flash the .bin File**  
Go to [releases](https://github.com/spacehuhn/wifi_ducky/releases) and download the right bin file for your ESP8266.  
You can flash it with the [esptool](https://github.com/espressif/esptool) or the [nodemcu-flasher](https://github.com/nodemcu/nodemcu-flasher).

**Upload using Arduino**  
Open the `esp8266_wifi_duck` sketch with [Arduino](https://www.arduino.cc/en/Main/Software).
You need to install the following libraries:
- [the latest ESP8266 SDK](https://github.com/esp8266/Arduino)
- [ESPAsyncWebServer](https://github.com/me-no-dev/ESPAsyncWebServer)
- [ESPAsyncTCP](https://github.com/me-no-dev/ESPAsyncTCP)

Then compile and upload it to your ESP8266 (check if your settings are right).

### Arduino ATmega32u4

Open the `arduino_wifi_duck` sketch in Arduino and upload it to your Arduino.  

### Wire everything up

Ok so now you need to connect the ESP8266 with the Arduino.  
Connect these pins:

| Arduino       | ESP82666      |
| ------------- |:-------------:|
| TX            | RX            |
| RX            | TX            |
| GND           | GND           |
| VCC (3.3V)    | VCC (3.3V)    |

Like I mentioned before, you'll need a 3.3V regulator if your Arduino only provides 5V.  
**Don't connect the ESP8266 to 5V!**  

If you use a plain ESP-12 like me, you also have to set the enable pin and to HIGH and GPIO15 to LOW:

| PIN          | Mode       |
| ------------ |:----------:|
| GPIO15       | LOW (GND)  |
| CH_PD (EN)   | HIGH (3.3V)|


### Update ESP8266 over the Web interface

Once you flashed the software, you can update it over the web interface.  
Go to `192.168.4.1/update` and upload the new .bin file.  
(In Arduino go to `Sketch`->`Export compiled Binary` to compile your own .bin file)  

## How to use it

Plug your Wi-Fi Ducky in and connect to the new Wi-Fi network `WiFi Duck`. The password is `quackquack`.  
Open your browser and go to `192.168.4.1`. 


#### This project is made off of spacehuhns wifi ducky project here [https://github.com/spacehuhn/wifi_ducky](https://github.com/spacehuhn/wifi_ducky)
