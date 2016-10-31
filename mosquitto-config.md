# Mosquitto Configuration

Now that you [installed](./installation.md) everything, let's configure it.

# Configure Mosquitto
If you install Mosquitto with the package manager, a default config file `/etc/mosquitto/mosquitto.conf` gets created. This file says it should load all `.conf` files from `/etc/mosquitto/conf.d/`. So we leave the default file in-place and create our own config in the config directory. Open a new config in your favorite editor (eg. nano) `sudo nano /etc/mosquitto/conf.d/iotserver.conf` and paste in the following config.

```
# specify the user mosquitto should use.
user mosquitto
# port mosquitto should listen to
port 1883
max_connections 300

# a password file and an access control list are optional (but required if you will be connecting mosquitto to the internet!)
# password_file /etc/mosquitto/users.pass
# acl_file /etc/mosquitto/acl

# You can configure extra listeners this way.
# Our Mosquitto should also support websockets.
listener 8884
protocol websockets
```

If you have set a `password_file` make sure it exists by creating at least one user for it. `sudo mosquitto_passwd -c /etc/mosquitto/users.pass new_mosquitto_username` the `-c` parameter means create new file, so only use that for the first user. [mosquitto_passwd](https://mosquitto.org/man/mosquitto_passwd-1.html) command explained.

If you have set an acl file, make sure it exists. `sudo nano /etc/mosquitto/acl` and paste the following (with your own changes). More info in the [manual](https://mosquitto.org/man/mosquitto-conf-5.html).

```
# No user defined (allow_anonymous), read all messages.
# topic  readwrite something/#
topic  read  #

# create user specific rights
# user name_of_user
# ... some topic rows here ...

# add some patterns, they count for everyone.
# %u is substituted with the username.
# %c is substituted with the clientId.
# allow each user to read/write his own namespace
pattern readwrite %u/#
```

Restart mosquitto `sudo service mosquitto restart`. Check all the ports your pi is listening to, to verify everything is running as expected `sudo netstat -plnt`.

# Test Mosquitto with [MQTT fx](http://mqttfx.jfx4ee.org)

Your Mosquitto server should be up and running at this moment. MQTT fx is a free open-source desktop client for mqtt. Start it up and configure your own server. I would suggest to create a separate account for each application but that is up to you.

First connect, then subscribe to `#` (means everything), then press scripts and execute the switch fountain test. It will send 20 messages that should also appear in subscribe tab.

# MQTT with TLS (recommended)
MQTT is a lightweight protocol without any form off data security. Everyone on the wire can intercept this traffic. While this may be OK in your home (private) network, if you connect your mqtt server to the internet, I would recommend only doing so for the mqtt listener with TLS enabled.

## 1a. Create your own self-signed certificate

This may need some explaining, but their are plenty of guides on the internet. (Pull request anyone?)

## 1b. Request StartSSL certificate

1. Download the ca-bundle `sudo curl -o /etc/mosquitto/certs/ca-bundle.crt https://www.startssl.com/certs/sca.server1.cr`
2. Create a certificate request (and save the key in `/etc/mosquitto/certs/`)
3. Download the certificate and save it to the same folder.
4. Edit `/etc/mosquitto/conf.d/iotserver.conf` and add the following:

```
# Secure MQTT listener.
listener 8883
cafile /etc/mosquitto/certs/ca-bundle.crt
certfile /etc/mosquitto/certs/certname.crt
keyfile /etc/mosquitto/certs/certname.key
tls_version tlsv1.2
```

## 2. Restart Mosquitto

If you change to configuration you will have to restart `sudo service mosquitto restart`. And verify everything is still running as expected `sudo netstat -plnt`.

# Install [Bridges and nodes](./bridges-and-nodes.md)

At this point you should have a working solution, that doesn't do much. Let's do something about it. By installing bridges and nodes you will get the ultimate home automation system.
