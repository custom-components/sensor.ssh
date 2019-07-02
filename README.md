# sensor.ssh
Generic SSH based sensor for Home Assistant
  
[![Version](https://img.shields.io/badge/version-0.1.2-green.svg?style=for-the-badge)](#) [![mantained](https://img.shields.io/maintenance/yes/2019.svg?style=for-the-badge)](#) [![forum](https://img.shields.io/badge/forum-visit-orange.svg?style=for-the-badge)](https://community.home-assistant.io/t/unifi-security-gateway/71505)   

Login to a remote server via ssh, execute a command and retrieve the result as sensor value

To get started download
```
/custom_components/ssh/__init__.py
/custom_components/ssh/sensor.py

```
into
```
<config directory>/custom_components/ssh/
```

**Example configuration.yaml:**

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
### Configuration Variables

**name**

  (string)(Optional) Friendly name of the sensor

**host**

  (string)(Required) The hostname or IP address of the remote server

**username**

  (string)(Required) A user on the remote server
  
**password**

(string)(Required) The password for the account

**port**

  (integer)(Optional) The port to ssh to
  Default value: 22

**command**

  (string)(Required) The command to execute on the remote server
  
### Considerations

The sensor utilises the pexpect library https://pexpect.readthedocs.io/en/stable/ which mimics a user logging into the remote server via ssh. This results in the output being formatted as output from a tty terminal. Check out the pexecpt documentation for the oddities this causes.

A sensor value can only by a maximum of 256 characters in length, therefore make use of the value_template to parse data larger than this.

