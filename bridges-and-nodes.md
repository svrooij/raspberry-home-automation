# Bridges

As explained in the readme, sadly enough most home automation devices don't speak mqtt (yet). But their are several bridges [available](https://github.com/mqtt-smarthome/mqtt-smarthome/blob/master/Software.md#interfaces). Set up the once you need, each of them got their own installation manual (if you're lucky).

The bridges I installed are listed [here](./hard-software.md#bridges)

## Creating your own bridge

Creating a bridge isn't really rocket science, if you get how it could work. It you take a look at [hue2mqtt](https://github.com/svrooij/hue2mqtt) you should have a good example. Every bridge roughly contains the following parts:

-  Some config file (for defining the mqtt server and hardware credentials).
-  MQTT client
-  Hardware (or api) interface.

The hue2mqtt bridge is written in Node.JS, and is pretty well documented. It has a function that polls for the latest statuses of all the lights, compares the state with the last state fetched by the bridge and publishes this state to mqtt (at `hue/status/light/lightname`) if it has changed.  This function will then schedule itself after 30 seconds with `setTimeout()`.

It also subscribes to `hue/set/light/lightname` to receive commands that need to be send to the Hue hardware. After which it calls the `publishHueStatus` function, so the new state also gets send to MQTT.

The same principal can be used for all kinds of devices, but has some delay. If the device supports pushing the data, you should create the bridge to listen for events and send those to mqtt. That would eliminate the delay, but for devices like thermostats or lights it doesn't seem to be a big problem. And the delay only exists if the device is controlled outside of the mqtt home automation system, something I try to eliminate anyway.

# Node RED nodes

You can add functionality to Node RED by adding nodes. The nodes I installed are described [here](./hard-software.md#extra-node-red-nodes), I would suggest those they are awesome. But if you want to add extra functionality you should definitely have a look at the [Node RED Library](http://flows.nodered.org).
