# unraid-mqtt-pub-sub
Unraid Plugin to add the ability to publish to a mqtt broker or subscribe to a topic.


## Installation
Plugins > Install Plugin (or it can be installed from the Community Apps plugin)
```
https://raw.githubusercontent.com/giganode/unraid-mqtt-pub-sub/master/mqtt-pub-sub.plg
```

## Usage

### Preparation
Enter your mqtt credentials here:
```
/boot/config/mqttcredentials
```

### Publishing
Start with this template:
```
#!/bin/bash

source /boot/config/mqttcredentials

if [[ -z "$MQTT_HOST" || -z "$MQTT_PORT" || -z "$MQTT_USER" || -z "$MQTT_PASSWORD" || -z "$MQTT_CLIENT_ID" ]]; then
  echo "Error: Information missing."
  exit 1
fi

mosquitto_pub -h $MQTT_HOST -p $MQTT_PORT -i $MQTT_CLIENT_ID -u $MQTT_USER -P $MQTT_PASSWORD -t "$MQTT_CLIENT_ID/sensor/voltage" -m "{\"voltage\": $value}"

```

### Subscribing
Start with this template:
```
#!/bin/bash

source /boot/config/mqttcredentials

if [[ -z "$MQTT_HOST" || -z "$MQTT_PORT" || -z "$MQTT_USER" || -z "$MQTT_PASSWORD" || -z "$MQTT_CLIENT_ID" ]]; then
  echo "Fehler: MQTT-Anmeldeinformationen sind unvollständig."
  exit 1
fi

mosquitto_sub -h $MQTT_HOST -p $MQTT_PORT -u $MQTT_USER -P $MQTT_PASSWORD -t "$MQTT_CLIENT_ID/sensor/voltage"

```

## Information
In this plugin, bc is included. It's useful when you need to do float calculations in your bash script. 
