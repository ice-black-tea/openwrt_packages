#
# Copyright (C) 2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=quectel-cm
PKG_RELEASE:=1

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel.mk

define Package/quectel-cm
  SECTION:=base
  CATEGORY:=Utilities
  TITLE:=Quectel LTE module dial tool
  DEPENDS:=+libc \
           +firewall \
		   +kmod-usb-core +kmod-usb-net +kmod-usb-net-cdc-ether \
		   +kmod-usb-net-cdc-mbim +kmod-usb-net-cdc-ncm +kmod-usb-net-cdc-subset \
		   +kmod-usb-net-qmi-wwan +kmod-usb-ohci  \
  		   +kmod-usb-serial +kmod-usb-serial-option +kmod-usb-serial-wwan \
		   +kmod-usb-uhci +kmod-usb2 \
		   +wwan +chat +ppp +uqmi +umbim \
		   +comgt +usb-modeswitch +usbutils \
		   +luci-proto-3g +luci-proto-ppp +luci-proto-qmi \
		   +isc-dhcp-client-ipv6
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Configure
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS) -Wall" \
		LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/quectel-cm/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/quectel-CM  $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/
	cp -pR ./root/* $(1)/
endef

$(eval $(call BuildPackage,quectel-cm))
