# Пакет xradio:
* Дрaйвер wifi радиомодуля: xr819
* поместить xradio в $(BUILD_DIR)/package/kernel
* пакет подтянет все зависимости во время зборки..

* cp 204-dts-wifi-add-xradio.patch -> $(BUILD_DIR)
* Скопировать фаил 204-dts-wifi-add-xradio.patch 
* в корневой каталог с исходиками $(BUILD_DIR). И с него дать команду:
```
patch -p1 < 204-dts-wifi-add-xradio.patch
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


* ===================================================================================
# Или можно будет воспользоваться уже пропатченными openwrt-master. Cделал зеркало с оpenwrt.
* Срез openwrt-master сделан-17.04.2019-20:30. И обновляться возможно не будет.
```
git clone https://github.com/melsem/openwrt.git openwrt-master
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make V=s
```

