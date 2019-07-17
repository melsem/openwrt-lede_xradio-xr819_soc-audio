# Пакет xradio для OpenWrt-master_kernel-4.19:
* Дрaйвер wifi радиомодуля: xr819
* поместить xradio в $(BUILD_DIR)/package/kernel
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

