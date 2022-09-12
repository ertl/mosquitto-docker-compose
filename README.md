![Mosquitto Logo](https://mosquitto.org/images/mosquitto-text-side-28.png 'Mosquitto')

# Simple Mosquitto broker

This is a simple [Mosquitto](https://mosquitto.org) broker to to quickly initialize projects requiring an MQTT broker. The config file is in the folder `config/mosquitto.conf`.

By default we activated the log and data persistance (respectively in `log` and `data` folder) and authentication.
The default user is `mosquitto/password`.
When authentication is activate also make sure you change the ip address in the mosquito.conf `listener 1883 192.168.0.16` to your ip address\range, which can accesss mosquitto.


**You always have to restart if you want the modification to be taken in account:**

```
docker-compose restart
```

# How to use

To start the container, just :

```
docker-compose up -d
```

The Mosquitto broker is now available on localhost. You can test it easily (require Mosquitto client):

| In one shell:

```
mosquitto_sub -h localhost -t "sensor/temperature"
```

| In a second shell:

```
mosquitto_pub -h localhost -t sensor/temperature -m 23
```

## Change user password / create a new user:

```
docker-compose exec mosquitto mosquitto_passwd -b /mosquitto/config/password.txt user password
```

## Delete user:

```
docker-compose exec mosquitto mosquitto_passwd -D /mosquitto/config/password.txt user
```
