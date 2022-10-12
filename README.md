# IoT - Adafruit IO - Arduino - Color Picker - Manual - Edward van Vliet

# Picking/determining a color via the Color Picker (Block) on Adafruit IO using a LED-strip connected to a NODEMCU 1.0, by using Arduino IDE (2.0) software.

By Edward van Vliet - 500761369<br>
Last updated 6 October 2022

## Introduction
Using this manual you'll be able to pick/determine a color via the Color Picker (Block) on Adafruit IO using a LED-strip connected to a NODEMCU 1.0, by using Arduino IDE (2.0) software.

## Required hardware components
  - 1x Node MCU 1.0
  - 1x LED-strip
  - 3x Jumper Wires glued to the end of the LED-strip
  - 1x USB-C to USB-B microcable (https://www.allekabels.nl/usb-c-kabel/11518/4080378/usb-c-naar-usb-b-micro-kabel.html?gclid=Cj0KCQjw1vSZBhDuARIsAKZlijQllk1tmEmzDAyOpEEB6p9cz1rm71ymovd92VNrhihNyiu-eR0gt8saAvW9EALw_wcB)
  
  
## Step 1: Connecting the Node MCU 1.0 to your laptop, and connect your LED-strip to the Node MCU 1.0
The first thing we want to do is connect our Node MCU to your laptop, using an USB-C to USB-B microcable. Then, we want to connect our LED-strip to the Node MCU, using Jumber Wires glued at the other end of the LED-strip. The image below shows which wires need to be connected to which pins on the board.

Leftmost pin to `3v3` (red wire)<br>
Second pin to `GND` (black wire)<br>
Right pin to `D5` (yellow wire)<br>

![Image of requirements](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/00_Required_Hardware_Components_20221010_125042_HDR.jpg)

## Step 2: Installing the required libraries in Arduino IDE
For the LED-strip to properly function, we will first need to install the required libraries in the [Arduino IDE](https://www.arduino.cc/en/main/software). We can do this by going to the 'Sketch' dropdown menu, selecting 'Include Library' and then clicking on 'Manage Libraries'.<br>

1. Go to the libraries tab that is the third button on the left. If your IDE verion is lower than 2.0, you can find this in Sketch > Include library > Manage libraries.
2. Here you search for "Adafruit IO Arduino". Watch out because sometimes the right one is not the one that pops up first.
3. Find the right one and click "Install" and then "Install All".

### Step 3: Setting up Adafruit IO

1. Go to https://io.adafruit.com/, click on "Get started for free" and make your account.
2. When your account is ready, click on "IO" in the navigation menu at the top of the page.
3. Click on the button with the yellow key icon.
![Image of your key and username in Adafruit IO](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/01_ADAFRUIT_IO_KEY_USERNAME.png)
4. Copy your key and remember your username for later use.

### Step 4: Creating Adafruit IO Feed and Color Picker

In Adafruit IO:
1. Go to Dashboards > New Dashboard, give it a name and create dashboard.
![Image of dashboard tab in Adafruit IO](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/02_Tab_DASHBOARDS.png)
2. Go to your newly made dashboard.
3. Create block using the settings button.
![Image of new block in Adafruit IO](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/03_Create_a_new_block_Color_Picker.png)
4. Choose "Colorpicker", and give it the feed name: "color"
![Image of feed name "color" in Adafruit IO](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/04_Create_Feed_name_color.png)
5. Create block.
6. Choose a color with your colorpicker.
![Image of how to choose a color in Adafruit IO](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/05_Choose_your_color_gold.png)<br>
![Image of your chosen color in Adafruit IO](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/06_Color_chosen_gold.png)


### Step 5: Adjust your code

In Arduino IDE:
1. Go to File > Examples > Adafruit IO Arduino > Adafruitio_14_neopixel.
![Image of Adafruitio_14_neopixexl file in Arduino IDE](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/07_Arduino_Examples_Adafruit_IO_Arduino_Adafruitio_14_neopixel.png)
2. Then click on the tab "config.h" in Arduino IDE, fill in your username and key like the example below.

```
#define IO_USERNAME "YOUR USERNAME HERE"
#define IO_KEY "YOUR KEY HERE"
```
![Image of config.h tab open in Arduino IDE](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/08_Arduino_config.h_opens.png)

3. Below that, you can fill in your WiFi SSID and Password.
(Advice: Use your phone's hotspot to prevent router problems, so you can use it everywhere. Also prevent using a 5GHz WiFi if possible.)<br>

```
#define WIFI_SSID "YOUR NETWORK NAME HERE"
#define WIFI_PASS "YOUR PASSWORD HERE"
```
![Image of WIFI_SSID and WIFI_PASS in code in Arduino IDE](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/09_Enter_IO_USERNAME_IO_KEY_WIFI_SSID_and_WIFI_PASS.png)

4. Change the PIN to "D5" and PIXEL_COUNT to the amount of lights your ledstrip have, like the example below.

```
#define PIXEL_PIN     D5
#define PIXEL_COUNT   18
```
![Image of PIN and PIXEL_COUNT in code in Arduino IDE](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/10_Set_PIXEL_PIN_5_to_PIXEL_PIN_D5.png)


### Step 6: Upload your code

1. Upload your code by clicking on the button with the arrow icon on the top left of your screen.
2. Activate the "Serial Monitor" with the magnifying glass button on the top right. Open the "Serial Monitor" on the bottom of your screen.
3. Put the Serial Monitor on 115200 baud.
4. If everything worked as planned, you will see that you're connected in the Serial Monitor. If not, try to use your mobile Hotspot WiFi, that worked for me.

### Step 7: Test your code

Change the color, by using the Color Picker on Adafruit IO. You could also use your mobile phone to change the color, try it out! Then you should see your LED-strip change to your chosen color.<br>



## Possible Errors:


## Error 1: Connection Error
If you keep seeing dots coming up on your Serial Monitor, it means something is wrong with the connection of your NodeMCU 1.0.
In my case the problem was the WiFi connection.
Because at first, I tried using my 5GHz (Home) WiFi throughout this whole process.
Unfortunately the Serial Monitor kept presenting me dots...

The dots that are appearing on your Serial Monitor means that your hardware, in this case my NodeMCU 1.0, can't properly connect to a WiFi network.
That's why it is highly recommended to use an own mobile hotspot, PREVENT using a 5GHz WiFi or hotspot! (According to [this source](https://arduino.stackexchange.com/questions/49370/esp8266-not-connecting-to-wifi) on Arduino Stack Exchange.)

## Solution to Error 1: Connection Error
Seeing the dots keep coming up on my Serial Monitor, I directly knew there was something wrong with the connection.
And then I searched about this connection error, and I found out I was not the only one with this problem.
Apparently according to [this article post about ESP WiFi problems](https://arduino.stackexchange.com/questions/49370/esp8266-not-connecting-to-wifi), the ESP8266 is not able to connect with 5Ghz WiFi.

So then I tried connecting the ESP8266 to my mobiel hotspot, on my smartphone. And fortunately, it worked!

