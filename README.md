<h1>Solis Inverters with Home Assistant</h1>

<h2>Summary Table</h2>

| Connection Type | DLS-W| DLS-L| S3-WiFi-ST| S2-WL-ST|
|:--|:--: |:--:|:--:|:--:|
|WiFi| Yes | No | Yes | Yes |
|LAN | No | Yes | No | Yes |
|SolisCloud| Yes | Yes | Yes | Yes |
| SolisCloud Remote Control | Yes*| Yes* | Yes |Yes |
| Home Assistant via SolarMan v5 | Yes | No | No | No |
| Home Assistant via Core Modbus TCP | No | Yes (3389) | No | Yes (502) |
| Home Assistant via SolaX Modbus Integration | No | Yes (3389) | No | Yes (502) |
| Home Assistant / SolisCloud Simultaneous | Yes | Yes | No | No |
| Home Assistant via Solis API | Yes | Yes | Yes | Yes |

**(*)** First reported working in April 2023; however, there are mixed messages from users complaining about the SolisCloud Remote Control with legacy dataloggers.

<h2>Current Data Loggers</h3>
These are currently being sold and supported by Solis:
<h3>S3-WiFi-ST</h3>

![S3](https://www.bimblesolar.com/image/cache/data/extra/xSolisW3-228x228.png.pagespeed.ic.hXxY06srvj.png)

This seems to be the most common datalogger supplied with new systems. WiFi only. With it, you can:

- Connect to SolisCloud (data at 5-minute intervals)
- Control the inverter via SolisClud remote control (https://solis-service.solisinverters.com/en/support/solutions/articles/44002373796-inverter-remote-control-application)
- Connect to Home Assistant using the read-only API integration at a 5-minute refresh: (https://github.com/hultenvp/solis-sensor)

Without additional hardware or its firmware modification, you cannot directly connect to Home Assistant via Modbus TCP.

To modify its firmware (do at your own risk):
- ginlong-solis: https://github.com/hn/ginlong-solis

You can get Home Assistant and Soliscloud without modifying its firmware if you follow this approach: https://github.com/alienatedsec/solis-ha-modbus-cloud

<h3>S2-WL-ST</h3>

![S2](https://www.solartradesales.co.uk/Cache/Images/Solis-Data-Logging-Stick-WL-4-Pin-03-500x500.jpg)

Less common but available to purchase in the UK. This has WiFi and wired LAN. With it, you can:

- Connect to SolisCloud (data at 5-minute intervals)
- Control the inverter via SolisClud remote control (https://solis-service.solisinverters.com/en/support/solutions/articles/44002373796-inverter-remote-control-application)
- Connect to Home Assistant using the read-only API integration at a 5-minute refresh: (https://github.com/hultenvp/solis-sensor)
- Connect directly to Home Assistant using the core Modbus TCP integration (https://github.com/fboundy/ha_solis_modbus) over TCP port 502
- Connect directly to Home Assistant using the SolaX Modbus TCP integration (https://github.com/wills106/homeassistant-solax-modbus) over TCP port 502

if you connect directly to the inverter from Home Assistant you will lose SolisCloud connectivity unless you use additional hardware such as this approach: https://github.com/alienatedsec/solis-ha-modbus-cloud

<h2>Legacy Data Loggers</h3>
These are no longer being sold or supported by Solis:
<h3>DLS-L</h3>

![DLS-L](https://statics3.solisinverters.com/uploads/image/5bdbe1df35b21.png)

These are LAN-only devices. What you can do with them seems to vary according to serial number but may include:
- Connect to SolisCloud (data at 5-minute intervals)
- Control the inverter via SolisClud remote control (https://solis-service.solisinverters.com/en/support/solutions/articles/44002373796-inverter-remote-control-application)
- Connect to Home Assistant using the read-only API integration at a 5-minute refresh: (https://github.com/hultenvp/solis-sensor)
- Connect directly to Home Assistant using the core Modbus TCP integration (https://github.com/fboundy/ha_solis_modbus) over TCP port 3389
- Connect directly to Home Assistant using the SolaX Modbus TCP integration (https://github.com/wills106/homeassistant-solax-modbus) over TCP port 3389

You may be able to access SolisCloud and Home Assistant simultaneously with these dataloggers


<h3>DLS-W</h3>

![DLS-W](https://s3.amazonaws.com/cdn.freshdesk.com/data/helpdesk/attachments/production/2043331447819/original/2Am8zHDI3Y6yjKemBgX7MRaVooxyUf3hZA.png?1650705272)

These are pretty much unobtainable now. They communicate using Modbus RTU encapsulated in the proprietary Solarman v5 protocol. To use these you need:

- pysolamanv5: https://github.com/jmccrohan/pysolarmanv5
- SolisMod: https://github.com/NosIreland/solismod
- home_assistant_solarman: https://github.com/StephanJoubert/home_assistant_solarman

<h2>Other Harwdware</h2>

There are a number of other direct ModBus approaches:

- Using an [Elfin EW11 and GC-1201K](https://github.com/Jumpy07/Solis---SolisCloud-and-Home-Assistant)
- Using [Waveshare Devices](https://github.com/alienatedsec/solis-ha-modbus-cloud)
- Using a [Raspberry Pi as a RS485 bridge](https://github.com/mjh-homeassistant/solis-multiplexer) 
