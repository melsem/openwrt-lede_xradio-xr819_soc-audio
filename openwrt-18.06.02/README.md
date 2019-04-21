# Patch dts-add-usb2-usb3-soc_codec-opi_zero-wifi_xradio_xr819_openwrt-18.06.02.patch

* cp dts-add-usb2-usb3-soc_codec-opi_zero-wifi_xradio_xr819_openwrt-18.06.02.patch -> dir-openwrt
* Скопировать фаил dts-add-usb2-usb3-soc_codec-opi_zero-wifi_xradio_xr819_openwrt-18.06.02.patch 
* в корневой каталог с исходиками <dir-openwrt>. И с него дать команду:
```
patch -p1 < dts-add-usb2-usb3-soc_codec-opi_zero-wifi_xradio_xr819_openwrt-18.06.02.patch
```
* Wifi "ON": cp add-on_wifi-mac80211.patch -> dir-openwrt
* Что бы включить WIFI еще до сборки, фаил add-on_wifi-mac80211.patch так же положить
* в корневой каталог с исходиками <dir-openwrt>. И с него дать команду:
```
patch -p1 < add-on_wifi-mac80211.patch
```
* Compile
```
make menuconfig
make V=s
```
* ===================================================================================
* Что бы включить каналы в alsamixer:
```
amixer -c 0 -q set "Line Out" 84%+ unmute &
amixer -c 0 -q set "DAC" 100%+ unmute &
```
* Что бы это автоматизировать надо еще прописать в /etc/rc.local

