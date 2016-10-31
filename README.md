# The Ultimate Home Automation system
This guide is based on a single opinion about how home automation could work.
I ([Stephan van Rooij](https://svrooij.nl)) started this guide, because I want to have my Home Automation system work for me. All the different apps for each kind of device are a hassle to use, and they don't work together.

If you don't want to read the introduction, go straight to the [Installation page](installation.md)

## Goals
For the ultimate home automation solution I have a few goals that I'm trying to reach:
-  One place that has ALL the information.
-  Combine data from different devices to a bigger picture.
-  Create rules for multiple devices at the same time.
-  Have the house respond to us (not) being at home.
-  A really nice looking interactive dashboard with all the information about the house and the ability to control it.

And the main requirement is that it should all run on a raspberry pi(3)! As this is a great platform for home automation.

# [MQTT](https://en.wikipedia.org/wiki/MQTT) to rule them all
MQTT is a lightweight messaging protocol developed in 1999 and standardised in 2013.

In this guide MQTT plays a really important part. A MQTT broker ([Mosquitto](https://mosquitto.org)) is going to be the center of this home automation system.

## Topics
MQTT works with topics (each application can subscribe to zero or more topics and can publish to different topics). This is a great way to express a status for a specific device. A single thermostat could use `themostat/living_room/status` to always publish it own status to. That way an application could listen to changes in the status of that thermostat and act on in. That same thermostat could listen to `thermostat/living_room/set` for commando's send to it.

## Bridges
Sadly enough most Home Automation devices like "Philips Hue", "Honeywell Evohome" or "Sonos", don't speak MQTT (yet, :wink:). So their should be bridges between MQTT and those hardware platforms.

This is where the [software list](https://github.com/mqtt-smarthome/mqtt-smarthome/blob/master/Software.md) from [MQTT-Smarthome](#mqtt-smarthome) comes in handy. It is a list of bridges between a different hardware platforms and MQTT.

Most of these bridges are scripts that run in the background on some machine (Raspberry in my case), that poll for updates every x seconds and publish the data to a specific topic. They also (like most bridges) support sending commands to a specific hardware platform by send a predefined command to one or more predefined topics.

# [MQTT-Smarthome](https://github.com/mqtt-smarthome/mqtt-smarthome)
The Ultimate Home Automation System is inspired by [MQTT-Smarthome](https://github.com/mqtt-smarthome/mqtt-smarthome). Two german guys designed the [Architecture](https://github.com/mqtt-smarthome/mqtt-smarthome/blob/master/Architecture.md) and made a list of [software](https://github.com/mqtt-smarthome/mqtt-smarthome/blob/master/Software.md). This guide won't duplicate their great information, so be sure to read their information as well!

# [Hardware and software used](./hard-software.md)

I've created a separate list of all the hardware and software used in this installation.

# [Continue to installation](./installation.md)

Enough introduction, let's get to work.
