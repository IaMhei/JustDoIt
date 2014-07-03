#
# Copyright (C) 2007-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ddns
PKG_VERSION:=r305
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-src.tar.gz
PKG_SOURCE_URL:=http://blog.a1983.com.cn/software/
PKG_MD5SUM:=8adc27cd1011a96a1a388e46a16ebdb3

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=DDNS client tool
  URL:=http://blog.a1983.com.cn
  DEPENDS:=+libpthread +libopenssl
endef

define Build/Configure
	(cd $(BUILD_DIR)/$(PKG_NAME); \
	./configure --prefix=/usr \
		    --without-peanuthull \
		    --without-dyndns \
	)
endef

define Build/Compile
	$(MAKE) -C $(BUILD_DIR)/$(PKG_NAME) \
	$(TARGET_CONFIGURE_OPTS) \
        LD="$(TARGET_CC)"
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_BIN) $(BUILD_DIR)/$(PKG_NAME)/ddns $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/
	$(INSTALL_DATA) ./files/ddns.config $(1)/etc/ddns.conf
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/ddns.init $(1)/etc/init.d/ddns
endef

define Package/$(PKG_NAME)/conffiles
/etc/ddns.conf
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
