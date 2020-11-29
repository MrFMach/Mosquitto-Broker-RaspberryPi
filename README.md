# Mosquitto-Broker-RaspberryPi
Mosquitto MQTT broker configuration on Raspberry Pi

#### Mosquitto Installation
Install the Mosquitto Broker that is available in the Debian archive, following what is described:
https://mosquitto.org/blog/2013/01/mosquitto-debian-repository/

After installing the Mosquitto broker, install the Mosquitto Clients

Install the Mosquitto Clients:
```
sudo apt install -y mosquitto-clients
```

Verify the status:
```
sudo systemctl status mosquitto.service
```
![](https://github.com/MrFMach/Mosquitto-Broker-RaspberryPi/blob/main/status.png)

You will see "active running".

***

#### Mosquitto User Authentication

Stop the broker:
```
sudo stop mosquitto
```

Create a user configuration file:
```
sudo mosquitto_passwd -c /etc/mosquitto/pwfile username
```
Replace "user" with your username. When confirming, you will be asked for a password. Type a password and confirm.

Open the Mosquitto configuration file:
```
sudo nano /etc/mosquitto/mosquitto.conf
```
Comment (#) the last line "include_dir /etc/mosquitto/conf.d"
And add the following lines:
```
password_file /etc/mosquitto/pwfile
allow_anonymous false
listener 1883
```

![](https://github.com/MrFMach/Mosquitto-Broker-RaspberryPi/blob/main/config.png)

This will allow only devices with a name and password to access port 1883.
Type Ctrl+X to exit and S to save.

Enable the service:
```
sudo systemctl enable mosquitto.service
```

Reboot the Raspberry Pi:
```
reboot
```

***

#### Mosquitto Broker Terminal Test

Open two terminals, one will be used for Subscribe and the other for Publish.

Do the following command on the first terminal:
```
mosquitto_sub -d -u username -P password -t topic/test.
```
This terminal will listen to the message that will come in the expected topic.

Now, do the command in the second terminal:
```
mosquitto_pub -d -u username -P password -t topic/test -m "Hello, Mosquitto!"
```
This terminal will publish the message in the configured topic.

![](https://github.com/MrFMach/Mosquitto-Broker-RaspberryPi/blob/main/pubsub.png)

If you got here, the broker is working correctly!!!

***
Thank you!

#### Fabio Machado
[![Linkedin Badge](https://img.shields.io/badge/-LinkedIn-blue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/fabio-machado-b932a476/)](https://www.linkedin.com/in/fabio-machado-b932a476/)

:computer:  Computer Engeneering  | :zap: Electronic  | :brazil:  Brazil

##### " cooperating, we'll go far " :rocket:
