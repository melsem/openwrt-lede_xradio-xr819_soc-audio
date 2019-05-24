# Пакет xradio для OpenWrt(Lede)-18.06.xx:
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

* ===================================================================================
* Что бы включить каналы в alsamixer:
```
amixer -c 0 -q set "Line Out" 84%+ unmute &
amixer -c 0 -q set "DAC" 100%+ unmute &
```
* Что бы это автоматизировать надо еще прописать в /etc/rc.local


