# MQTT-2-RPints_GoWithTheFlowMeters_and_DS18B20
NodedMCU (ESP8266), Dual YF-S201 Flow Meters and DS18B20 OneWire MQTT Integration with RaspberryPints

---

To set=up MQTT/RPints integration using an ESP8266 microcontroller,
Please reference:
https://github.com/Garzlok/RaspberryPints/blob/garzlok_rpi/README.md

This sketch will allow a user of a NodeMCU to attach 2 YF-5201 Flow Meters, and a DS18B20 OneWire Temperature Sensor and integrate with the RandR+ RaspberryPints branch via MQTT.

Current Pin Assignments:

D0

D1 

D2 (Flow Meter 1)

D3 

D4 

3V3 

GND 

D5 (Flow Meter 2)

D6 

D7 (DS18B20 Data)

D8 

RX

TX

GND (Flow Meter GND)

3V3 (Flow Meter 3V3)

___

A0

RSV

RSV

SD3

SD2

SD1

CMD

SD0

CLK

GND

3V3

EN

RST

GND (DS18B20 GND)

VIN (DS18B20 VIN) ---->4.7KOhm<----- (DS18B20 Data)

---

-DS18B20 Sensor will broadcast temperature every 15 min via MQTT to RaspberryPints

-Sensor Payload that RaspberryPints expects:

-"T;probe;temp;unit;timestamp"

-Flow Meters will only broadcast when a pour is initiated

-Minimum of 15 pulses is needed to achieve actual pour (can be adjusted in the sketch)

-Flow Meter Payload that RaspberryPints expects:

-"P;UserID;tapnumber;pourpulses"

-The UserID is set to -1, which in most cases will not correspond to a user. Change to a preferred UserID
