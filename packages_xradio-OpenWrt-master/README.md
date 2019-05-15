# Пакет xradio для OpenWrt-master:
* Дрaйвер wifi радиомодуля: xr819
* поместить xradio в $(BUILD_DIR)/package/kernel
* пакет подтянет все зависимости во время зборки..
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
* Срез openwrt-master сделан-15.05.2019-13:30.
```
git clone https://github.com/melsem/openwrt.git openwrt-master
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make V=s
```

