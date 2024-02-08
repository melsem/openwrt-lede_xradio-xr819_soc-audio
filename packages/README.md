# An example of how to enable wifi (xradio-xr819) for Orangepi-Zero (OpenWrt 22.03.6).

1. Download the old stable firmware image 'OpenWrt 22.03.6' for MMC: [https://downloads.openwrt.org/releases/22.03.6/targets/sunxi/cortexa7/openwrt-22.03.6-sunxi-cortexa7-xunlong_orangepi-zero-ext4-sdcard.img.gz](https://downloads.openwrt.org/releases/22.03.6/targets/sunxi/cortexa7/openwrt-22.03.6-sunxi-cortexa7-xunlong_orangepi-zero-ext4-sdcard.img.gz)

2. Write it down on MMS. And insert the flash drive into the OrangePi slot.

3. To connect OrangePi to the Internet you need:
* Connect the OrangePi “LAN” cable to the “LAN” of the router that distributes the Internet.
* OrangePi and the PC are connected to a router that distributes the Internet.

4. Connect UART0 OrangePi to PC. Power on +5V.
* And from the console run the commands:
```
uci set network.@device[0].ports="usb0"
uci set network.lan.ipaddr="192.168.10.1"
uci set network.wan=interface
uci set network.wan.proto='dhcp'
uci set network.wan.device='eth0'
uci commit network
```
* And we allow access to OrangePi from the “WAN” zone:
```
uci set firewall.@zone[1].input='ACCEPT'
uci commit firewall
```
Restarting the firewall and network:
```
/etc/init.d/firewall reload
/etc/init.d/network reload
```
* Let's check if there is Internet in OrangePI:
```
ping -w5 8.8.8.8
```
* If the pings were successful, something like this will happen:
```
root@OpenWrt:/# ping -w5 8.8.8.8
PING 8.8.8.8 (8.8.8.8): 56 data bytes
64 bytes from 8.8.8.8: seq=0 ttl=117 time=31.927 ms
64 bytes from 8.8.8.8: seq=1 ttl=117 time=31.809 ms
64 bytes from 8.8.8.8: seq=2 ttl=117 time=32.111 ms
64 bytes from 8.8.8.8: seq=3 ttl=117 time=31.617 ms
64 bytes from 8.8.8.8: seq=4 ttl=117 time=32.174 ms
```
* Install packages:
```
cd /tmp
opkg update

opkg install kmod-xradio_5.10.201+2023-05-10-a2dd9cd8-1_arm_cortex-a7_neon-vfpv4.ipk
opkg install boot-config_1.5-09.01.2024_arm_cortex-a7_neon-vfpv4.ipk
opkg install busybox_1.35.0-231125.65937_arm_cortex-a7_neon-vfpv4.ipk

reboot

boot-config overlays wifi
```
*** Example write in spi-flash 16MB for orangepi-zero. ***
```
boot-config overlays fullflash
```
