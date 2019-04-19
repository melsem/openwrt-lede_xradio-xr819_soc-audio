# Patch dts-add-usb2-usb3-soc_codec-opi_zero-wifi_xradio_xr819_openwrt-master.patch

* cp dts-add-usb2-usb3-soc_codec-opi_zero-wifi_xradio_xr819_openwrt-master.patch -> dir-openwrt
* Скопировать фаил dts-add-usb2-usb3-soc_codec-opi_zero-wifi_xradio_xr819_openwrt-master.patch 
* в корневой каталог с исходиками <dir-openwrt>. И с него дать команду:
```
patch -p1 < dts-add-usb2-usb3-soc_codec-opi_zero-wifi_xradio_xr819_openwrt-master.patch
```
* Wifi "ON": cp add-on_wifi-mac80211.patch -> dir-openwrt
* Что бы включить WIFI еще до сборки, фаил add-on_wifi-mac80211.patch так же положить
* в корневой каталог с исходиками <dir-openwrt>. И с него дать команду:
```
patch -p1 < add-on_wifi-mac80211.patch
```
* Compile
```
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make V=s
```
* Что бы включить каналы в alsamixer:
```
amixer -c 0 -q set "Line Out" 84%+ unmute &
amixer -c 0 -q set "DAC" 100%+ unmute &
```


# Или можно будет воспользоваться уже пропатченными openwrt-master. Cделал зеркало с оpenwrt.
* Срез openwrt-master сделан-17.04.2019-20:30. И обновляться возможно не будет.
```
git clone https://github.com/melsem/openwrt.git openwrt-master
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make V=s
```

