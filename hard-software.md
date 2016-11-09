# Hardware & Software

This page will list all the hardware & software used in this guide.

## Hardware

- Raspberry Pi 3
- USB wall socket
- 32GB SD card
- UTP cable (wired connections are always better!)

## OS & Software

The default choice for the raspberry is Rasbian so I've started with [Rasbian Jessie lite](https://www.raspberrypi.org/downloads/raspbian/).

- Rasbian Jessie lite (v2016-09-23)
- [Mosquitto](https://mosquitto.org) (as a mqtt broker)
- [Node.JS](https://nodejs.org/en/) needed for Node RED and my bridges.
- [Node RED](https://nodered.org) as a easy-to-use but still advanced rule engine.

## Bridges

As stated in the [README](./README.md), sadly enough most home automation devices don't support mqtt (yet). So I installed the following bridges to interact with my current hardware platforms.

- [**evohome2mqtt**](https://github.com/svrooij/evohome2mqtt) connects my evohome system to mqtt. (And is actually the second MQTT bridge I developed.)
- [**hue2mqtt**](https://github.com/svrooij/hue2mqtt) connects all my Philips hue lights to mqtt. I've created this bridge even though their was one [available](https://github.com/owagner/hue2mqtt), but the latter was in java, something I didn't want to install on my Pi.
- [**kodi2mqtt**](https://github.com/owagner/kodi2mqtt) This [Kodi](https://kodi.tv) plugin makes kodi talk mqtt about status changes.
- [**mqtt-camera-ftpd**](https://github.com/stjohnjohnson/mqtt-camera-ftpd) is a FTP server that you can use in combination with the picture upload functionality on your IPCAM. This way events (motion or sound if supported) from your IPCAM get published to your MQTT server.

## Extra Node RED [nodes](https://flows.nodered.org)

-  [node-red-dashboard](https://flows.nodered.org/node/node-red-dashboard) create fancy dashboards in matter of minutes.
-  [node-red-node-darksky](https://flows.nodered.org/node/node-red-node-darksky) quickly download weather information.
