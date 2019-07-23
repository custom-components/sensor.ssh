## Generic SSH sensor

Allows execution of an arbitrary command via ssh the results of which can be filtered by the use of a value template.

A sensor value can only by a maximum of 256 characters in length, therefore make use of the value_template to parse data larger than this.

## Example configuration.yaml:

```yaml
sensor:
  - platform: ssh
      host: !secret proxmox_host
      name: 'NUC CPU Temp'
      username: !secret proxmox_user
      password: !secret proxmox_pass
      command: "sensors | grep 'Package id 0:' | cut -c17-20"
      value_template: >-
        {%- set line = value.split("\r\n") -%}
        {{ line[1] }}
      unit_of_measurement: "ºC"
```
