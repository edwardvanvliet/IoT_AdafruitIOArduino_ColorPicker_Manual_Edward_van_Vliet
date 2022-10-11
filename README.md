# IoT - Adafruit IO - Arduino - Color Picker - Manual - Edward van Vliet

# Picking/determining a color via the Color Picker (Block) on Adafruit IO using a LED-strip connected to a NODEMCU 1.0, by using Arduino IDE (2.0) software.

By Edward van Vliet<br>
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
Second pin to `D5` (yellow wire)<br>
Third pin to `GND` (black wire)<br>

![Image of requirements]()

## Step 2: Installing the required libraries in Arduino IDE
For the LED-strip to properly function, we will first need to install the required libraries in the [Arduino IDE](https://www.arduino.cc/en/main/software). We can do this by going to the 'Sketch' dropdown menu, selecting 'Include Library' and then clicking on 'Manage Libraries'.<br>

![Image of requirements](https://github.com/edwardvanvliet/IoT_AdafruitIOArduino_ColorPicker_Manual_Edward_van_Vliet/blob/main/images/01_ADAFRUIT_IO_KEY_USERNAME.png)
