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
  
![Image of requirements]()
  
## Step 1: Connecting the DHT11 Sensor to the Arduino Board
The first thing we want to do is connect our DHT11 Sensor to the Arduino Board, using Jumber Wires. The image below shows which wires need to be connected to which pins on the board. Note that we also have to attach the resistor between the wires that are connected to `3v3` and `D2`.

Leftmost pin to `3v3` (red wire)<br>
Second pin to `D5` (yellow wire)<br>
Third pin empty<br>
Fourth pin to `GND` (black wire)<br>
Resistor between red and green wire<br>
![Image of schematic](https://github.com/Ralphvandodewaard/manualiot/blob/master/schematic1.png)

## Step 2: Installing the required libraries in Arduino IDE
For the DHT11 Sensor to properly function, we will first need to install the required libraries in the [Arduino IDE](https://www.arduino.cc/en/main/software). We can do this by going to the 'Sketch' dropdown menu, selecting 'Include Library' and then clicking on 'Manage Libraries'.<br>

In the Library Manager, we first want to search for 'Adafruit Unified Sensor'. Scroll down to the correct library, made by Adafruit, and press 'Install'. If done correctly, the library will now say 'Installed'.<br>
![Image of library manager2](https://github.com/Ralphvandodewaard/manualiot/blob/master/library2.png)

We now want to install one more library, called the 'DHT sensor library' by Adafruit. Search for the correct library in the Library Manager and again press 'Install'. If done correctly, the library will now say 'Installed'.<br>
![Image of library manager3](https://github.com/Ralphvandodewaard/manualiot/blob/master/library3.png)

## Step 3: Uploading the required code for the DHT11 Sensor to the Arduino Board
We can now start uploading code to our Arduino Board to get the DHT11 Sensor to work. Plug your Arduino Board into your computer using a USB to Micro USB cable and copy and paste the code shown below to the Arduino IDE. If the required libraries for the sensor have been properly installed, as done in step 2, you can now press 'Upload' in the top left of your screen. The code will start compiling and uploading to your Arduino Board.

When doing this, make sure that in 'Tools' the correct Board and Port is selected. In our case the Board is set to 'NodeMCU 1.0', while the Port depends on which USB input you're using.
```
#include "DHT.h"

#define DHTPIN 4
#define DHTTYPE DHT11

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);

  dht.begin();
}

void loop() {
  delay(10000);

  float h = dht.readHumidity();
  float t = dht.readTemperature();

  if (isnan(h) || isnan(t)) {
    Serial.println("Failed to read");
    return;
  }

  Serial.print("Humidity: ");
  Serial.print(h);
  Serial.println("%");
  Serial.print("Temperature: ");
  Serial.print(t);
  Serial.println("°C");
  Serial.println("");
}
```
## Step 4: Reading data from the DHT11 Sensor
If all steps so far have been succesfully executed, we will now be able to see the data gathered by our DHT11 Sensor. This can be done in the serial monitor in the Arduino IDE, by pressing the button in the top right of your screen. If everything functions properly, you will be able to read multiple measurements of the humidity and temperature in the serial monitor. When doing this, make sure that the selection dropdown in the bottom right is set to '9600 baud'. 

![Image of serial monitor](https://github.com/Ralphvandodewaard/manualiot/blob/master/serial.png)

## Step 5: Connecting the Servo Motor to the Arduino Board
Now that we've got our DHT11 Sensor working, we want to connect the Servo Motor to our Arduino Board. The Servo Motor that we use has three wires and needs to be connected to the Arduino Board as shown in the image below.

Brown wire to `GND`<br>
Red wire to `3v3`<br>
Orange wire to `D4`<br>

![Image of schematic2](https://github.com/Ralphvandodewaard/manualiot/blob/master/schematic2.png)

## Step 6: Uploading the required code for the Servo Motor to the Arduino Board
Unlike with the DHT11 Sensor, the required library for the Servo Motor comes pre-installed on the Arduino IDE. We can therefore start uploading the code for our Servo Motor to the Arduino Board straight away. The code below combines both the code for the DHT11 Sensor and the Servo Motor, so make sure to replace the current code instead of adding to it. Then again press 'Upload' in the top left of your screen. The code will start compiling and uploading to your Arduino Board.

```
#include "DHT.h"
#include <Servo.h>

#define DHTPIN 4
#define DHTTYPE DHT11

DHT dht(DHTPIN, DHTTYPE);

Servo servo;  
int servoPin = 2;
int angle = 0;
float threshold = 65;
int window = 0;

void setup() {
  Serial.begin(9600);

  dht.begin();
  servo.attach(servoPin); 
}

void loop() {
  delay(10000);

  float humidity = dht.readHumidity();
  float temperature = dht.readTemperature();

  if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Failed to read");
    return;
  }

  Serial.print("Humidity: ");
  Serial.print(humidity);
  Serial.println("%");
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println("°C");
  
  if (humidity >= threshold && window == 0) {
    for(angle = 0; angle < 180; angle++) {                                  
      servo.write(angle);               
      delay(15);
    }
    window = 1;
    Serial.println("Window open");
  } else if (humidity < threshold && window == 1) {
    for(angle = 180; angle > 0; angle--) {                                  
      servo.write(angle);               
      delay(15);
    } 
    window = 0;
    Serial.println("Window closed"); 
  }

  Serial.println("");
}
```

## Step 7: Test and customize
If the Servo Motor has been connected properly and the new code has been uploaded to the Arduino Board, you should now see that the Servo Motor starts to rotate when the measured humidity reaches a certain threshold. You can try this yourself by blowing into the DHT11 Sensor to increase the measured humidity. 

Now that everything is working, you can start editing the code to your liking for your own projects. Below are just a few examples of changes or additions you could make:
- Change the `delay`, which is now set to 10000, or 10 seconds
- Change or set new thresholds based on the measured humidity and temperature. The `threshold` variable is currently set to 65% humidity
- Use another form of output instead of the Servo Motor, like LED Lights
- Create an overview of your measured data and make graphs using [Adafruit](https://learn.adafruit.com/adafruit-io-basics-dashboards/overview)
