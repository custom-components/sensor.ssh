## Generic SSH sensor

Allows execution of an arbitrary command via ssh the results of which can be filtered by the use of a value template.

Note that the size of a sensor value if limited to 255 characters, if you need to process more than this a custom component or a script is the way to go.

## Example configuration.yaml:

```yaml
# Example configuration.yaml entry to return the first 3 lines of the specified command
sensor:
  - platform: ssh
    host: 192.168.0.1
    username: username
    password: password
    command: 'show vpn ipsec sa'
    value_template: >-
      {%- set line = value.split("\r\n") -%}
      {{ line[1] + line[2] + line[3] }}
```
