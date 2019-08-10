# Пакет xradio для OpenWrt(Lede)-18.06.xx: (kernel<=4.14.95)
* Дрaйвер wifi радиомодуля: xr819
* пакет подтянет все зависимости во время зборки..

* Поместить add-patch_dts_file-wifi-xradio.patch в $(BUILD_DIR)
* и дать команду:
```
patch -p1 < add-patch_dts_file-wifi-xradio.patch
```

* Compile
```
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make V=s
```
