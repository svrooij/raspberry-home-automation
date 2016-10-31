# Install the Ultimate Home Automation system (on a pi3).

This guide is not a full script to run and have a working system for you. I just try to send you in the right direction.

# Clean Raspbian Jessie lite

It is recommended to start clean for this project. You don't want an unstable Home automation system because you did some experimenting with your Pi in the past.

1. [Download](https://www.raspberrypi.org/downloads/raspbian/) a Rasbian Jessie lite image.
2. Write it to a SD card.
3. Run the config wizard `sudo rasp-config`, for all the standard stuff. Enlarge filesystem, change hostname (choose wisely), change the default password `raspberry` and turn on SSH for remote management.
4. Update the system with the latest updates. `sudo apt-get update` and `sudo apt-get upgrade`.

# Install Mosquitto

Mosquitto is going to be the MQTT broker, and will be the central part of our home automation system. [Open Source Hardware lab](https://oshlab.com/install-mqtt-mosquitto-raspberry-pi/) has a great guide on how to install Mosquitto on a raspberry.

We will be configuring this later on. The default installation doesn't have any listeners configured.

```
curl -s https://repo.mosquitto.org/debian/mosquitto-repo.gpg.key | sudo apt-key add -
sudo curl -o /etc/apt/sources.list.d/mosquitto-jessie.list http://repo.mosquitto.org/debian/mosquitto-jessie.list
sudo apt-get update
sudo apt-get install mosquitto

```

# Install NodeJS

Node.JS is needed for Node RED and for at least 1 brdige. Install Node.JS with the following script. Found on [this page](https://nodejs.org/uk/download/package-manager/#debian-and-ubuntu-based-linux-distributions).

```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

# Install Node RED

Because we are using the latest version of Node.JS, we cannot use apt-get to install node-red. So use this command, found [here](http://nodered.org/docs/hardware/raspberrypi#install-node-red).

```
sudo npm cache clean
sudo npm install -g --unsafe-perm  node-red
```

## Run Node RED on reboot

We didn't use the package manager to install node red, so you have to add it as a service manually. The needed script is found [here](http://nodered.org/docs/hardware/raspberrypi#adding-autostart-capability-using-systemd).

# Installation complete? Let's configure.

If you followed the instructions on this page, you should now have the following:

-  Clean raspbian jessie lite install.
-  Node.JS working
-  Mosquitto installed (not working).
-  Node RED running (http://ip_of_pi_or_hostname:1880) check it out.

Open the [Mosquitto configuration](mosquitto-config.md) to setup mosquitto correctly.
