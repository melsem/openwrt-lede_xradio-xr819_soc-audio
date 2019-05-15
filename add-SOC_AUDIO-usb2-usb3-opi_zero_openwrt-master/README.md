# Patch add-SOC_AUDIO-usb2-usb3-opi_zero_openwrt-master.patch
* Включит встроенное SOC-AUDIO

* cp add-SOC_AUDIO-usb2-usb3-opi_zero_openwrt-master.patch -> dir-openwrt
* Скопировать фаил add-SOC_AUDIO-usb2-usb3-opi_zero_openwrt-master.patch
* в корневой каталог с исходиками <dir-openwrt>. И с него дать команду:
```
patch -p1 < add-SOC_AUDIO-usb2-usb3-opi_zero_openwrt-master.patch
```
* Wifi "ON": cp add-on_wifi-mac80211.patch -> dir-openwrt
* Что бы включить WIFI еще до сборки, фаил add-on_wifi-mac80211.patch так же положить
* в корневой каталог с исходиками <dir-openwrt>. И с него дать команду:
```
patch -p1 < add-on_wifi-mac80211.patch
```

* Compile
```
make clean
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


* ===================================================================================
# Или можно будет воспользоваться уже пропатченными openwrt-master. Cделал зеркало с оpenwrt.
* Срез openwrt-master сделан-15.05.2019-13:30.
```
git clone https://github.com/melsem/openwrt.git openwrt-master
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make V=s
```

