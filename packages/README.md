# An example of how to enable wifi (xradio-xr819) for Orangepi-Zero (OpenWrt 22.03.6 Linux version 5.10.201).

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
wget https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/packages/kmod-xradio_5.10.201+2023-05-10-a2dd9cd8-1_arm_cortex-a7_neon-vfpv4.ipk
wget https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/packages/busybox_1.35.0-231125.65937_arm_cortex-a7_neon-vfpv4.ipk
wget https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/packages/boot-config_1.5-09.01.2024_arm_cortex-a7_neon-vfpv4.ipk
opkg install kmod-xradio_5.10.201+2023-05-10-a2dd9cd8-1_arm_cortex-a7_neon-vfpv4.ipk
opkg install boot-config_1.5-09.01.2024_arm_cortex-a7_neon-vfpv4.ipk
opkg install busybox_1.35.0-231125.65937_arm_cortex-a7_neon-vfpv4.ipk
reboot

boot-config overlays wifi
```
* And to enter the OrangePi settings from an http browser, you need to find out what IP address:
```
ifconfig | sed -n '/eth0\(.*\)Link/,/Interrupt\:/p' | sed -n 's/.*inet addr\:\(.*\)  Bcast.*/\1/p'
```
* Something like this will happen:
```
root@OpenWrt:~# ifconfig | sed -n '/eth0\(.*\)Link/,/Interrupt\:/p' | sed -n 's/.*inet addr\:\(.*\)  Bcast.*/\1/p'
192.168.22.215
root@OpenWrt:~# 
```

* ** Example write in spi-flash 16MB (w25q128 (16384 Kbytes)) for orangepi-zero. ***
```
boot-config overlays fullflash
cd /tmp
wget https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/packages/openwrt-sunxi-cortexa7-xunlong_orangepi-zero-lts-squashfs-fullflash.bin
mtd -e fullflash write openwrt-sunxi-cortexa7-xunlong_orangepi-zero-lts-squashfs-fullflash.bin fullflash
```
* And now, without MMC-flash, it will boot from a 16MB spi-flash.

