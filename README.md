# GNU/Linux tricks for Maastricht University
This repository contains commands and configs I found useful regarding the use of
University services. Some of these may be distro-specific so your mileage may vary.

Mentions of `<student id>` refer to the UM username, e.g. `i6123456` including the
`i`.

## Eduroam
### Netctl
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

## VPN
### OpenConnect
[OpenConnect](https://wiki.archlinux.org/index.php/OpenConnect) can be used to
connect to the University VPN, for instance to gain access to journals.

Installation on Arch:
```
sudo pacman -S openconnect
```
Installation on Debian/Ubuntu/Mint:
```
sudo apt-get install openconnect
```

Having installed it simply run:
```
sudo openconnect vpn.maastrichtuniversity.nl -u <student id>
```
Type in your password, and you're in!

### EZproxy
Alternatively, you may use [EZproxy](https://www.oclc.org/nl/ezproxy.html) from
within your browser for access to literature as described
[here](https://linuxunimaas.blogspot.com/2013/11/reading-literature-from-home-with-your.html).

## File service
The University file service is accessible with
[Samba](https://wiki.archlinux.org/index.php/samba). Note that it seems you need to
be physically present and connected to the university Eduroam to make use of the file
services.

You can use `smbclient` to get a list of network drives:
```
smbclient -L mfs.maastrichtuniversity.nl -U <student id>
```

You may use CIFS (e.g. install `cifs-utils` on Arch) to mount the drives directly.
In order to mount your private drive directory in `/media/unimaas/userdata` run:
```
# Create a mountpoint
sudo mkdir -p /media/unimaas/userdata
# Mount it
sudo mount -t cifs //mfs.maastrichtuniversity.nl/users/students/<student id>/data /media/unimaas/userdata -o username=<student id>@unimaas.nl,vers=2.0,uid=$(id -u),gid=$(id -g)
```

More information may be found in the [ICTS Manual - UM drive
   mappings](https://kb-icts-maastrichtuniversity-nl.ezproxy.ub.unimaas.nl/display/ISM/Manual+File+Service+-+Mapping+UM+network+drives+in+Windows).

# Useful resources
 - [Linux @ Maastricht University blog](https://linuxunimaas.blogspot.com/)
 - [ICTS
   Manual from within
   MAASnet](https://kb.icts.maastrichtuniversity.nl/display/ISM/ICTS+Servicedesk+Manuals)
   and [by
   proxy](https://kb-icts-maastrichtuniversity-nl.ezproxy.ub.unimaas.nl/display/ISM/ICTS+Servicedesk+Manuals)

