# An example of how to enable wifi (xradio-xr819) for Orangepi-Zero: 
- * OpenWrt-v22.03.6 Linux version 5.10.201 - mac80211_5.10.201+5.15
- * Or OpenWrt-v23.05.2 Linux version 5.15.137 - mac80211_5.15.137+6.1.24
- 
- * Speed test of Wi-Fi client “xradio-xr819” for OpenWrt-05.23.2 (mac80211_5.15.137+6.1.24).
```
root@orangepi-zero:~# speedtest-netperf.sh -H netperf-west.bufferbloat.net -p 1.1.1.1 --sequential
2024-03-19 00:21:20 Starting speedtest for 60 seconds per transfer session.
Measure speed to netperf-west.bufferbloat.net (IPv4) while pinging 1.1.1.1.
Download and upload sessions are sequential, each with 5 simultaneous streams.
.............................................................
 Download:  19.17 Mbps
  Latency: [in msec, 61 pings, 0.00% packet loss]
      Min:  52.880
    10pct:  70.048
   Median: 167.131
      Avg: 204.035
    90pct: 365.500
      Max: 436.577
 CPU Load: [in % busy (avg +/- std dev) @ avg frequency, 57 samples]
     cpu0:   8.2 +/-  6.1  @ 1008 MHz
     cpu1:   5.5 +/-  4.6  @ 1001 MHz
     cpu2:   8.2 +/-  5.2  @ 1001 MHz
     cpu3:   8.0 +/-  6.3  @  998 MHz
 Overhead: [in % used of total CPU available]
  netperf:   2.0
...............................................................
   Upload:  15.69 Mbps
  Latency: [in msec, 63 pings, 0.00% packet loss]
      Min:  53.000
    10pct:  67.848
   Median:  75.844
      Avg:  76.951
    90pct:  87.094
      Max: 108.161
 CPU Load: [in % busy (avg +/- std dev) @ avg frequency, 59 samples]
     cpu0:   9.0 +/-  7.6  @ 1008 MHz
     cpu1:   7.3 +/-  6.1  @ 1002 MHz
     cpu2:   6.8 +/-  6.8  @ 1008 MHz
     cpu3:   6.0 +/-  6.1  @ 1008 MHz
 Overhead: [in % used of total CPU available]
  netperf:   1.1
root@orangepi-zero:~# 
```
- 
1. Download the old stable firmware image 'OpenWrt 22.03.6' for MMC: [https://downloads.openwrt.org/releases/22.03.6/targets/sunxi/cortexa7/openwrt-22.03.6-sunxi-cortexa7-xunlong_orangepi-zero-ext4-sdcard.img.gz](https://downloads.openwrt.org/releases/22.03.6/targets/sunxi/cortexa7/openwrt-22.03.6-sunxi-cortexa7-xunlong_orangepi-zero-ext4-sdcard.img.gz)
- * Or 
1. Download the old stable firmware image 'OpenWrt 23.05.2' for MMC: [https://downloads.openwrt.org/releases/23.05.2/targets/sunxi/cortexa7/openwrt-23.05.2-sunxi-cortexa7-xunlong_orangepi-zero-ext4-sdcard.img.gz](https://downloads.openwrt.org/releases/23.05.2/targets/sunxi/cortexa7/openwrt-23.05.2-sunxi-cortexa7-xunlong_orangepi-zero-ext4-sdcard.img.gz)
- 
- 
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
- 
# Example: OpenWrt 22.03.6 Linux version 5.10.201 - mac80211_5.10.201+5.15
* Install packages:
```
cd /tmp
opkg update
wget https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/packages/kmod-xradio_5.10.201-2023-05-10-a2dd9cd8-1_arm_cortex-a7_neon-vfpv4.ipk
wget https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/packages/busybox_1.35.0-231125.65937_arm_cortex-a7_neon-vfpv4.ipk
wget https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/packages/boot-config_1.5-09.01.2024_arm_cortex-a7_neon-vfpv4.ipk
opkg install kmod-xradio_5.10.201-2023-05-10-a2dd9cd8-1_arm_cortex-a7_neon-vfpv4.ipk
opkg install boot-config_1.5-09.01.2024_arm_cortex-a7_neon-vfpv4.ipk
opkg install busybox_1.35.0-231125.65937_arm_cortex-a7_neon-vfpv4.ipk
reboot

boot-config overlays wifi
reboot
```
- 
# Example: OpenWrt 23.05.2 Linux version 5.15.137 - mac80211_5.15.137+6.1.24
* Install packages:
```
cd /tmp
opkg update
wget https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/packages/kmod-xradio_5.15.137-2023-05-10-a2dd9cd8-1_arm_cortex-a7_neon-vfpv4.ipk
wget https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/packages/busybox_1.36.1-1_arm_cortex-a7_neon-vfpv4.ipk
wget https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/packages/boot-config_1.5-09.01.2024_arm_cortex-a7_neon-vfpv4.ipk
opkg install kmod-xradio_5.15.137-2023-05-10-a2dd9cd8-1_arm_cortex-a7_neon-vfpv4.ipk
opkg install boot-config_1.5-09.01.2024_arm_cortex-a7_neon-vfpv4.ipk
opkg install busybox_1.36.1-1_arm_cortex-a7_neon-vfpv4.ipk
reboot

boot-config overlays wifi
reboot
```
- 
- 
- * And to enter the OrangePi settings from an http browser, you need to find out what IP address:
```
ifconfig | sed -n '/eth0\(.*\)Link/,/Interrupt\:/p' | sed -n 's/.*inet addr\:\(.*\)  Bcast.*/\1/p'
```
- * Something like this will happen:
```
root@OpenWrt:~# ifconfig | sed -n '/eth0\(.*\)Link/,/Interrupt\:/p' | sed -n 's/.*inet addr\:\(.*\)  Bcast.*/\1/p'
192.168.22.215
root@OpenWrt:~# 
```
  ![boot-config](https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/blob/master/packages/18.png)
  ![boot-config](https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/blob/master/packages/26.png)
  ![boot-config](https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/blob/master/packages/33.png)

#  ** Example write in spi-flash 16MB (w25q128 (16384 Kbytes)) for orangepi-zero. OpenWrt 22.03.6 ***
- * Connect UART0 OrangePi to PC. Power on +5V.
- * And from the console run the commands:
```
boot-config overlays fullflash
reboot
cd /tmp
wget https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/packages/openwrt-sunxi-cortexa7-xunlong_orangepi-zero-lts-squashfs-fullflash.bin
mtd -e fullflash write openwrt-sunxi-cortexa7-xunlong_orangepi-zero-lts-squashfs-fullflash.bin fullflash
```
- * And now, without MMC-flash, it will boot from a 16MB spi-flash.
