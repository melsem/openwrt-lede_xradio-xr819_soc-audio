# sunxi: Allwinner H2+ (OPi Zero) add package xradio:
* Пакет xradio можно использовать в openwrt-master и openwrt(lede)-18.06.xx

* Дрaйвер wifi радиомодуля xr819:
* пакет подтянет все зависимости во время зборки..

* Поместить xradio в $(BUILD_DIR)/package/kernel
* cp 204-dts-wifi-add-xradio.patch -> $(BUILD_DIR)/package/kernel
* Скопировать фаил 204-dts-wifi-add-xradio.patch 
* в корневой каталог с исходиками $(BUILD_DIR). И с него дать команду:
```
patch -p1 < 204-dts-wifi-add-xradio.patch

make clean
make menuconfig
make V=s
```
