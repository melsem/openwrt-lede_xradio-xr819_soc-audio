# Patch dts-add-usb2-usb3-soc_codec-opi_zero-wifi_xradio_xr819_openwrt-master.patch

* 1) cp dts-add-usb2-usb3-soc_codec-opi_zero-wifi_xradio_xr819_openwrt-master.patch -> dir-openwrt
```
patch -p1 < dts-add-usb2-usb3-soc_codec-opi_zero-wifi_xradio_xr819_openwrt-master.patch
```
* Wifi "ON": cp add-on_wifi- mac80211.patch -> dir-openwrt
```
patch -p1 < add-on_wifi- mac80211.patch
```
* Compile
```
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make V=s
```
