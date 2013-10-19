Raspberry Pi Setup (Raspbian)
=============================

## Installation (MacOSX procedure)

1. **Find the device:** `diskutil list` without the card and then again with the card. A new `/dev/disk#` should have appeared. That's the SD card. Instead of using that exact device, use /dev/**r**disk#, which is a raw path, with less extra processing.
2. **Unmount device:** `diskutil unmountDisk /dev/disk#`
3. **Copy image into disk:** `sudo dd bs=1m if=<IMAGE HERE>.img of=/dev/rdisk#`
4. **Eject device:** `sudo diskutil eject /dev/rdisk#`

Have fun!

## Wifi

1. Edit `/etc/network/interfaces`, and insert:

```
auto lo

iface lo inet loopback
iface eth0 inet dhcp

auto wlan0
allow-hotplug wlan0
iface wlan0 inet dhcp
        wpa-ssid "SSID_here"
        wpa-psk "password_here"
```

2. ***optional*** - If you want to define a static DHCP lease, edit `/etc/dhcp/dhclient.conf`, and insert:

```
alias {
  interface "wlan0";
  fixed-address 192.168.1.200;
}
```

You can change the IP address.


## Regenerate SSH SSL keys

1. Run `rm /etc/ssh/ssh_host*`
2. Run `dpkg-reconfigure openssh-server`

## No-IP (dynamic DNS)

- Create an account in [No-IP](http://www.no-ip.com/)
- `cd /usr/local/src/`
- `wget http://www.no-ip.com/client/linux/noip-duc-linux.tar.gz`
- `tar xf noip-duc-linux.tar.gz`
- `cd noip-2.1.9-1/`
- `make install`
- Add `/usr/local/bin/noip2` to `/etc/rc.local` before `exit 0` so it starts after reboot.

You can check the status with `/usr/local/bin/noip2 -S`, start the service with `/usr/local/bin/noip2` and kill it with `/usr/local/bin/noip2 -K <pid>` (get pid from -S).

If you need to recreate the default config file, run `sudo /usr/local/bin/noip2 -C`.

## Node.js

http://blog.rueedlinger.ch/2013/03/raspberry-pi-and-nodejs-basic-setup/
