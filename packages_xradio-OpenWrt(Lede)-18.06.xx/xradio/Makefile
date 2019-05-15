include $(TOPDIR)/rules.mk

PKG_NAME:=xradio
PKG_RELEASE=2

PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define Download/xr819
  FILE:=xr819.tar.bz2
  URL:=https://github.com/melsem/openwrt-lede_xradio-xr819_soc-audio/raw/master/firmware/
  HASH:=add13a7045cb2dbf170d51e2be678e0af8e2c7bf29cfd0f33a3a216fc88696dc
endef
$(eval $(call Download,xr819))

define KernelPackage/xradio
  SUBMENU:=Wireless Drivers
  TITLE:=Xradio xr819: test wifi-openwrt-18.06.xx
  DEPENDS:=@TARGET_sunxi +kmod-mac80211 +wpad-mini
  FILES:=$(PKG_BUILD_DIR)/xradio_wlan.ko
  AUTOLOAD:=$(call AutoProbe,xradio_wlan)
endef

NOSTDINC_FLAGS = \
	-I$(PKG_BUILD_DIR) \
	-I$(STAGING_DIR)/usr/include/mac80211-backport/uapi \
	-I$(STAGING_DIR)/usr/include/mac80211-backport \
	-I$(STAGING_DIR)/usr/include/mac80211/uapi \
	-I$(STAGING_DIR)/usr/include/mac80211 \
	-include backport/autoconf.h \
	-include backport/backport.h

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C "$(LINUX_DIR)" \
		$(KERNEL_MAKE_FLAGS) \
		$(PKG_MAKE_FLAGS) \
		SUBDIRS="$(PKG_BUILD_DIR)" \
		NOSTDINC_FLAGS="$(NOSTDINC_FLAGS)" \
		modules
endef

define KernelPackage/xradio/install
	$(INSTALL_DIR) $(1)/lib/firmware/xr819
	$(TAR) -C $(1)/lib/firmware -xjf $(DL_DIR)/xr819.tar.bz2
endef

$(eval $(call KernelPackage,xradio))
