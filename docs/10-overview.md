# Objective of the Lecture

The objective of this lecture is to provide a first introduction to the,
[Internet of Things](https://en.wikipedia.org/wiki/Internet_of_things) (IoT).
To achieve this objective a, ESP8266-based micro controller is used.
This micro controller is connected to a temperature and humidity sensor. Using,
[ESPHome](http://esphome.io/), data form this sensor is transmitted to the
[Simple IoT Stack](https://github.com/ceedee666/simple-iot-stack/) using
the [MQTT protocol](https://mqtt.org). The IoT stack contains different services
like a database for storing sensor values. The data is then analysed using
[grafana](https://grafana.com/) or custom [Jupyter](https://jupyter.org/)
notebooks.

## Passwords and Password Managers

If you put devices or service on the internet it is important to consider
security. Here is just one, example of what can happen if you are not
careful: (https://www.reddit.com/r/aws/comments/8rj9ep/my_aws_account_was_hacked/)!

Consequently, it is very important that:

- You need to make sure that you **never** publicly expose login information or
  certificated related to your AWS account.,
- You always use strong passwords. Here is an nice example of weak and strong passwords:
  ![XKCD Password Strength](https://imgs.xkcd.com/comics/password_strength.png),

### Password Manager

In my opinion the only sensible way to handle passwords is the usage of a
password manager. With a password manager it is possible to use an individual
passwords for every services. Furthermore, long and secure passwords can
automatically be generated by password managers.

Wikipedia has a nice [list of password managers](https://en.wikipedia.org/wiki/List_of_password_managers)
including a detailed feature comparison. I currently use [Bitwarden](https://en.wikipedia.org/wiki/Bitwarden).
For additional security you should also enable
[two-factor authentication](https://en.wikipedia.org/wiki/Multi-factor_authentication) whenever possible.

## Navigation

- [Next Section ➡️](./20-esphome-intro.md)