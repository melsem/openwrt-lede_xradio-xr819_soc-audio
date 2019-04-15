# Openwrt-18.06 Orange-Pi-Zero ADD drivers wifi xradio-xr819, soc-audio.

* 1. Поместить Openwrt-18.06_add-opizero_ON-xradio-xr819_soc-audio_usb2_usb3_spi.patch в корневой каталог с сырцами
* И с каталога дать комманду:
``
patch -p1 < Openwrt-18.06_add-opizero_ON-xradio-xr819_soc-audio_usb2_usb3_spi.patch
```
* 2. Поместить архив ?????.tar.xz в корневом каталоге в /dl
* 3. И все.. make menuconfig > Kernel modules > Wireless Drivers отметить
```
<m> kmod-xradio
  ```
* > Kernel modules > Sound Support отметить
  ```
* <m> kmod-sound-soc-sunxi
* <m> kmod-sound-soc-sun8i-codec
* <m> kmod-sound-soc-sun8i-codec-analog
  ```
* Exit and save.

* 4.
```
make clean
```
* У меня почему то выскакивала ошибка пока не сделал make clean

* 5.
```
make V=s
```

* 6. Потом не забыть вписать на работающей самой системе opi-zero в rc.local
```
amixer -c 0 -q set "Line Out" 84%+ unmute &
amixer -c 0 -q set "DAC" 84%+ unmute &
exit 0
```
