# Linux tricks for Maastricht University
This repository contains commands and configs I found useful regarding the use of
University services. Some of these may be distro-specific so your mileage may vary.

## Eduroam
Below is a config for `netctl` that works with Eduroam.

`/etc/netctl/wlp3s0-eduroam`
```
Description='eduroam'
Connection=wireless
Interface=wlp3s0
Security=wpa-configsection
ESSID=eduroam
TimeoutWPA=10
IP=dhcp
WPAConfigSection=(
	'ssid="eduroam"'
	'proto=WPA2'
	'key_mgmt=WPA-EAP'
	'eap=PEAP'
	'phase2="auth=MSCHAPV2"'
	'identity="<student id>@unimaas.nl"'
	'password="<password>"'
)
```
