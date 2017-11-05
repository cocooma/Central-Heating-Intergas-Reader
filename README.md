# Central-Heating-Intergas-Reader

This project has been replaced by https://github.com/keesma/Intergas-Central-Heating-Monitor-Homie
The new version has much faster communication, a smaller codebase and also can do OTA.

* This program can read the the status of a Central heating from Intergas.
  It has been built for an esp8266.
  The central heating status is sent through MQTT to a central system (MQTT broker).
  
* Pre-release: This version has first been tested for several weeks on a breadboard with an Intergas Prestige CW6. It has run stable for some weeks. 

* Configuration
  The following needs to be configured (see config.h):
  - WiFi access point: SSID and password
  - MQTT broker server name; username and password authentication is used
  - NTP server (pool) name

* Connect esp8266 to Intergas

  I have included a diagram how to connect the optocouplers (and a picture of the prototype).

  To connect the central heating to the esp8266.
  It is best to use an optocoupler to connect the esp8266 to the Intergas.
  E.g. an 4n25 can be used (take two 4n25s to protect both tx and rx).
  I got good results by using a 220 Ohm resistor for the input and a 1k Ohm resistor in the output.

  Default config on the esp8266 is:
  - pin 4: Rx
  - pin 5: Tx
  - pin 12: LED. The LED is on during initialization and while sending data to the Intergas.
  The communication speed is 9600 baud.

  The intergas has a 4 pin plug with: Vcc, ground, Tx and Rx.

* Dependencies
  - MQTT: PubSubClient for communication with MQTT broker
  - Timezone, Timelib: for time calculations
  - SoftwareSerial: for serial communications (so the intergas serial communication does not interfere with firmware loading and info/debug messages)
  - WifiUdp: for communcation for UDP (needed for UTP)

* Openhab: I have connected the esp8266 through MQTT to openhab. Openhab can display the data, save it and create nice graphs. The item definitions are included. The rules are required for translating the status bytes to (bit) values.

* Time: the time is synchronised with an NTP server (server (or pool) name can be configured in config.h). A timer runs how long the program has been running, so you can see if it was restarted unexpectedly.

* Power: My esp8266 has a separate 3.3V power supply. The Intergas may supply power but prefer not the experiment with that (it only supplies power to one of the optocouplers).
