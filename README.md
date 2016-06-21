# Examples of Prototyping Physical Interactions with VR

Code samples for a quick and easy approach to prototyping physical interactions with mobile VR.

This system uses an Arduino microcontroller with WIFI, a node server, and a VR app built in Unity to a mobile platform (Google Cardboard or Gear VR).  All of these need to be on the same wifi network.

The node server offers a REST interface to receive messages from the arduino and connects to the Unity app using socket.io.

There are many different ways to connect a microcontroller wirelessly to a Unity app, including ones that don't rely on an intermediary server.  The advantages of this method are: simple, cheap, reliable and easy to debug.  Having the intermediate server lets you monitor the communication flow between your Arduino and your Unity app, and allows you to test each component individually.  It is particularly useful when doing live demos, as it gives you a continuous health check, and lets you send commands directly to Unity, for example, to reset the game state without removing the phone from the VR headset.


## Software and Hardware

**You'll need the following:**

* A wifi microcontroller that can be programmed using Arduino.  Sample code is written for the Arduino Yun and the Adafruit Huzzah ESP8266 module.  

**Yun**:  the Yun must first be configured to connect to your wifi network.  When the Yun first starts up, if it can't find a wifi network it knows how to connect to, it will create its own network, with a name like ArduinoYun-XXXXXXXXXXXX. Connect to that network, and then open the Yun config page at http://arduino.local or 192.168.240.1. After a few moments, a web page will appear asking for a password. Enter "arduino" and click the Log In button.  Then click the "Configure" button.  You'll be able to configure a name and password for your Yun, and also select a wifi network and log in to that.  After you click the Configure & Restart button, the Yun will kill its own wifi network and connect to the one you specified.  (Much more detail on setting up and using a Yun is at: https://www.arduino.cc/en/Guide/ArduinoYun).  

The sketch we will run on the Yun uses the Process class of the Bridge library.  This lets us run commands on the linux processor part of the Yun.  We will call the "curl" command to access our REST server.  More info on the Yun Bridge library is here: https://www.arduino.cc/en/Reference/YunBridgeLibrary

**ESP8266**: Off-the-shelf these come with a Lua interpreter installed.  But you can use Arduino to program them, by following these instructions: https://learn.adafruit.com/adafruit-huzzah-esp8266-breakout/using-arduino-ide.

I recommend the Adafruit HUZZAH ESP8266 breakout or the Feather HUZZAH.  The former requires an FTDI adapter for USB programming.  This board from Tinkersphere looks like it will do about the same thing (and has built-in usb): http://tinkersphere.com/electronic-components/1388-nodemcu-esp8266-iot-board.html.  Sparkfun also has a similar board.

The sketch for the ESP8266 boards uses the ESP8266WiFi, ESP8266WiFiMulti, and ESP8266HTTPClient libraries, which you will install through the "Manage Libraries" tool in the Arduino IDE.

* On your computer, install node.js.  The code uses the socket.io and node-simple-router libraries.

* In Unity, we use the SocketIO plugin by Fabio Panettieri.


This project basically provides the plumbing between whatever kind of controller you build with your arduino, and the VR experience you build in Unity. For the purposes of demonstrating how it works, I've provided code assuming that you have two tilt switches attached to your arduino (put them perpendicular to each other, so a "throw" motion would trigger each in quick succession.)  And I've given you a basic Unity scene with some cardboard boxes, and a collection of balls you can throw.

If you want to use tilt swtiches, I'd recommend these:
http://tinkersphere.com/sensors/750-tilt-switch.html
http://tinkersphere.com/sensors/1013-mercury-tilt-switch-6mm.html




