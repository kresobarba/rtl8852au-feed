include $(TOPDIR)/rules.mk

PKG_NAME:=rtl8852au
PKG_RELEASE:=1

PKG_LICENSE:=GPLv2
PKG_LICENSE_FILES:=

PKG_SOURCE_URL:=https://github.com/lwfinger/rtl8852au.git
PKG_MIRROR_HASH:=865ab0fa91471d595c283d2f3db323f7f15455f5 
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2024-05-06
PKG_SOURCE_VERSION:=865ab0fa91471d595c283d2f3db323f7f15455f5

PKG_MAINTAINER:=Andriy Utkin & Larry Finger <hello@autkin.net>
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/rtl8852au
  SUBMENU:=Wireless Drivers
  TITLE:=The driver supports rtl8832au/rtl8852au chipsets
  DEPENDS:=+kmod-cfg80211 +kmod-usb-core +@DRIVER_11AC_SUPPORT  
  FILES:=$(PKG_BUILD_DIR)/8852au.ko
  AUTOLOAD:=$(call AutoProbe,rtl8852au)
  PROVIDES:=kmod-rtl8852au
endef

NOSTDINC_FLAGS := \
	$(KERNEL_NOSTDINC_FLAGS) \
	-DCONFIG_IOCTL_CFG80211 -DRTW_USE_CFG80211_STA_EVENT -DBUILD_OPENWRT \
	-DCONFIG_LITTLE_ENDIAN

define Build/Compile
	+$(KERNEL_MAKE) $(PKG_JOBS) \
		M="$(PKG_BUILD_DIR)" \
		NOSTDINC_FLAGS="$(NOSTDINC_FLAGS)" \
		-I$(KERNEL_BUILD_DIR)/include \
		CONFIG_RTL8852AU=m \
		modules
endef

# never got this to work, but it's an appealing approach
#define Build/Compile
#	+$(MAKE) \
#		-C "$(PKG_BUILD_DIR)" \
#		$(KERNEL_MAKE_FLAGS) \
#		KSRC="$(LINUX_DIR)" \
#		src="$(PKG_BUILD_DIR)" \
#		NOSTDINC_FLAGS="$(NOSTDINC_FLAGS)" \
#		modules
#endef
$(eval $(call KernelPackage,rtl8852au))
