include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

PKG_NAME:=kmod-rtw89-usb
PKG_VERSION:=5.11.1
PKG_RELEASE:=1
PKG_MAINTAINER:=You <you@example.com>
PKG_LICENSE:=GPL-2.0
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/morrownr/rtw89.git
PKG_SOURCE_VERSION:=main
PKG_MIRROR_HASH:=skip
PKG_BUILD_PARALLEL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/kernel.mk

define KernelPackage/kmod-rtw89-usb
  SUBMENU:=Wireless Drivers
  TITLE:=Realtek 8852/8852B USB WiFi driver (rtw89)
  DEPENDS:=+kmod-cfg80211 +kmod-mac80211 +kmod-usb-core
  FILES:=$(PKG_BUILD_DIR)/rtw89usb.ko
  AUTOLOAD:=$(call AutoProbe,rtw89usb)
endef

define KernelPackage/kmod-rtw89-usb/description
  Realtek rtw89 USB WiFi driver with full AP and client mode support.
endef

define Build/Prepare
	$(call Build/Prepare/Default)
endef

define Build/Compile
	$(MAKE) -C "$(KERNEL_BUILD_DIR)" \
		M="$(PKG_BUILD_DIR)/usb" \
		CONFIG_RTW89_USB=y \
		modules
endef

define Build/Clean
	$(MAKE) -C "$(KERNEL_BUILD_DIR)" M="$(PKG_BUILD_DIR)/usb" clean
endef

$(eval $(call KernelPackage,kmod-rtw89-usb))
