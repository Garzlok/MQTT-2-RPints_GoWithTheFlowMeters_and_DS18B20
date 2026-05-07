# MQTT-2-RPints_ESP32-All In One
LolinD32 (ESP32), MFRC522 RFID, Dual YF-S201 Flow Meters and DS18B20 OneWire MQTT Integration with RaspberryPints

---

To set=up MQTT/RPints integration using an ESP8266 microcontroller,
Please reference:
https://github.com/Garzlok/RaspberryPints/blob/garzlok_rpi/README.md

---

This sketch will allow a user of a Lolin D32 to attach 1 MFRC522 RFID, 2 YF-5201 Flow Meters, and a DS18B20 OneWire Temperature Sensor and integrate with the RandR+ RaspberryPints branch via MQTT.

Component Pin----------------------Lolin D32 Pin---------------------Note

MFRC522 (RFID)3.3V-----------------MFRC522 (RFID)3V3-----------------MFRC522 (RFID)Do NOT use 5V.

GND--------------------------------GND

RST--------------------------------GPIO 0

SDA (SS)---------------------------GPIO 5

SCK--------------------------------GPIO 18---------------------------Standard SPI Clock.

MISO-------------------------------GPIO 19---------------------------Standard SPI MISO.

MOSI-------------------------------GPIO 23---------------------------Standard SPI MOSI.

DS18B20 (Temp)VCC------------------DS18B20 (Temp)3V3-----------------DS18B20 (Temp)

GND--------------------------------GND

DATA-------------------------------GPIO 27---------------------------Use 4.7kΩ pull-up to 3V3.

YF-S201 (Both)Red (VCC)------------YF-S201 (Both)USB (5V)------------YF-S201 (Both) Flow meters need 5V.

YF-S201 (Both)Black (GND)----------YF-S201 (Both)--------------------TF-S201 (Both) Flow Meters need Grounded

YF-S201 (Flow 1) Yellow (SIG)------GPIO 25 YF-S201 (Flow 1)

YF-S201 (Flow 2) Yellow (SIG)------GPIO 26 YF-S201 (Flow 2)


---

-DS18B20 Sensor will broadcast temperature every 15 min via MQTT to RaspberryPints

-Sensor Payload that RaspberryPints expects:

-"T;probe;temp;unit;timestamp"

-Flow Meters will only broadcast when a pour is initiated

-Minimum of 15 pulses is needed to achieve actual pour (can be adjusted in the sketch)

-Flow Meter Payload that RaspberryPints expects:

-"P;tagIDStatus;tapnumber;pourpulses;RFIDTag"

-tagIDStatus is known as UserID in RaspberryPints

-If no RFID Card is used, tagIDStatus is sent as "-1" which in most cases will not correspond to a user.

-If an RFID Card is used, tagIDStatus is sent as "", which RaspberryPints will determine User ID based on the RFID Tag.

-RFID Information will only be broadcasted in the Flow Meter Payload

-45 seconds after scanning the card, RFID information in RFIDTag will be removed from memory


