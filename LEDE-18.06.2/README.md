* Openwrt-lede18.06.02 Orange-Pi-Zero ADD drivers wifi xradio-xr819

* 1. Поместить LEDE-18.06.2_add-opizero_ON-xradio-xr819_usb2_usb3_ir_spi.patch в корневой каталог с сырцами
* 2. И с каталога дать комманду: patch -p1 < LEDE-18.06.2_add-opizero_ON-xradio-xr819_usb2_usb3_ir_spi.patch
* 3. Поместить архив backports-2019-03-13.tar.xz в корневом каталоге в /dl
* 4. И все.. make menuconfig > Kernel modules > Wireless Drivers отметить <m> kmod-xradio
* Exit and save.
* 7. И что бы только пакеты пересобрать: make package/compile V=s
