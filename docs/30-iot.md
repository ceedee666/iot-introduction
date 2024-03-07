# Connecting to an IoT Platform

This part of the tutorial assumes the availability of a IoT platform containing
at least a MQTT broker and some database. In this description I will use the
[Simple IoT Stack](https://github.com/ceedee666/simple-iot-stack).

The installation of the Simple IoT Stack on a VM in the Oracle cloud is
shown in this video.

[![Installation des IoT Stacks](https://img.youtube.com/vi/_bjv4_a2idU/hqdefault.jpg)](https://www.youtube.com/embed/_bjv4_a2idU)

## Step 1: Measure temperature and humidity

```yaml
# Temp & Humidity Sensor
sensor:
  - platform: dht
    pin: D6
    temperature:
      name: "Temperature"
      id: temp
    humidity:
      name: "Humidity"
      id: humi
```

The complete YAML file including the temperature sensor is available [here](../src/iot-getting-started-04.yaml)

## Step 2: Sending measurements to MQTT broker

```yaml
# MQTT
mqtt:
  broker: !secret mqtt_host
  port: 1883
  username: !secret mqtt_user
  password: !secret mqtt_password

interval:
  - interval: 1min
    then:
      - mqtt.publish_json:
          topic: "environment/d1_mini"
          payload: |-
            root["temp"]=id(temp).state;
            root["humi"]=id(humi).state;
      - logger.log:
          format: "Sending sensor values - temp: %.1f - humi: %.1f"
          args: [id(temp).state, id(humi).state]
```

The complete YAML file including sending data to the MQTT broker is available [here](../src/iot-getting-started-05.yaml)

## Step 3: Controlling the LED via MQTT

```yaml
# MQTT
mqtt:
  broker: !secret mqtt_host
  port: 1883
  username: !secret mqtt_user
  password: !secret mqtt_password
  on_message:
    - topic: led/d1mini
      payload: "on"
      then:
        - light.turn_on: red_led
    - topic: led/d1mini
      payload: "off"
      then:
        - light.turn_off: red_led

interval:
  - interval: 1min
    then:
      - mqtt.publish_json:
          topic: "environment/d1_mini"
          payload: |-
            root["temp"]=id(temp).state;
            root["humi"]=id(humi).state;
      - logger.log:
          format: "Sending sensor values - temp: %.1f - humi: %.1f"
          args: [id(temp).state, id(humi).state]
```

The complete YAML file including the possibility to control the LED with
MQTT messages is available [here](../src/iot-getting-started-06.yaml)
