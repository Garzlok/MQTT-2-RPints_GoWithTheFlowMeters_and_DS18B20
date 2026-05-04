# MQTT-2-RPints_GoWithTheFlowMeters_and_DS18B20
NodedMCU (ESP8266), MFRC522 RFID, Dual YF-S201 Flow Meters and DS18B20 OneWire MQTT Integration with RaspberryPints

---

To set=up MQTT/RPints integration using an ESP8266 microcontroller,
Please reference:
https://github.com/Garzlok/RaspberryPints/blob/garzlok_rpi/README.md

---

This sketch will allow a user of a NodeMCU to attach 1 MFRC522 RFID, 2 YF-5201 Flow Meters, and a DS18B20 OneWire Temperature Sensor and integrate with the RandR+ RaspberryPints branch via MQTT.

Current Pin Assignments:
D0 (Unused)                          |                      A0
D1 (Flow Meter 1)                    |                     RSV
D2 (Flow Meter 2)                    |                     RSV
D3 (RFID RST_PIN)                    |                     SD3
D4 (DS18B20 Data)-----------|        |                     SD2
3V3 (RFID 3v30              |        |                     SD1
GND (RFID GND)              |        |                     CMD
D5 (RFID MISO)              |        |                     SD0
D6 (RFID MOSI)              |        |                     CLK
D7 (RFID sck)           (4.7K Ohm)   |                     GND
D8 (RFID SS_Pin)            |        |                     3V3
RX                          |        |                      EN
TX                          |        |                     RST
GND (Flow Meter GND)        |        |       (DS18B20 GND) GND
3V3 (Flow Meter 3V3)--------|        |        (DS18B20VIN) VIN

DS18B20 Sensor will broadcast temperature every 15 min via MQTT to RaspberryPints
Sensor Payload that RaspberryPints expects:
"T;probe;temp;unit;timestamp"
Flow Meters will only broadcast when a pour is initiated
Minimum of 15 pulses is needed to achieve actual pour (can be adjusted in the sketch)
Flow Meter Payload that RaspberryPints expects:
"P;tagIDStatus;tapnumber;pourpulses;RFIDTag"
tagIDStatus is known as UserID in RaspberryPints
If no RFID Card is used, tagIDStatus is sent as "-1" which in most cases will not correspond to a user.
If an RFID Card is used, tagIDStatus is sent as "", which RaspberryPints will determine User ID based on the RFID Tag.
RFID Information will only be broadcasted in the Flow Meter Payload
30 seconds after scanning the card, RFID information in RFIDTag will be removed from memory

