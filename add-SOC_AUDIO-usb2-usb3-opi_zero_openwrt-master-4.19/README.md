# Patch add-SOC_AUDIO-usb2-usb3-opi_zero_openwrt-master.patch
* Включит встроенное SOC-AUDIO openwrt-master kernel-4.19

* cp add-SOC_AUDIO-usb2-usb3-opi_zero_openwrt-master.patch -> dir-openwrt
* Скопировать фаил add-SOC_AUDIO-usb2-usb3-opi_zero_openwrt-master.patch
* в корневой каталог с исходиками <dir-openwrt>. И с него дать команду:
```
patch -p1 < add-SOC_AUDIO-usb2-usb3-opi_zero_openwrt-master.patch
```
* Wifi "ON": cp add-on_wifi-mac80211.patch -> dir-openwrt
* Что бы включить WIFI еще до сборки, фаил add-on_wifi-mac80211.patch так же положить
* в корневой каталог с исходиками <dir-openwrt>. 
* И с него дать команду:
```
patch -p1 < add-on_wifi-mac80211.patch
```

* Compile
```
make clean
make menuconfig
make V=s
```

