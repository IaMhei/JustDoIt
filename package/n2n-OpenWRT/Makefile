#
# Copyright (C) 2007-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_BRANCH:=trunk
PKG_SOURCE_URL:=https://svn.ntop.org/svn/ntop/trunk/n2n
PKG_REV:=$(shell LC_ALL=C svn info ${PKG_SOURCE_URL} | sed -ne's/^Revision: //p')

PKG_NAME:=n2n
PKG_VERSION:=$(PKG_REV)
PKG_RELEASE:=2

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_SOURCE_PROTO:=svn
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/n2n/Default
  SECTION:=net
  CATEGORY:=Network
  URL:=http://www.ntop.org/n2n/
endef

define Package/n2n_v1
  $(call Package/n2n/Default)
  TITLE:=VPN tunneling daemon(V1)
  DEPENDS:=+libpthread +kmod-tun
endef

define Package/n2n_v2
  $(call Package/n2n/Default)
  TITLE:=VPN tunneling daemon(V2)
  DEPENDS:=+libpthread +kmod-tun +libopenssl
endef

define Build/Compile
	+$(MAKE) -C $(PKG_BUILD_DIR)/n2n_v1/ \
		$(TARGET_CONFIGURE_OPTS) \
		CFLAGS="$(TARGET_CFLAGS)" \
		INSTALL_PROG=":"

	+$(MAKE) -C $(PKG_BUILD_DIR)/n2n_v2/ \
		$(TARGET_CONFIGURE_OPTS) \
		CFLAGS="$(TARGET_CFLAGS) $(TARGET_LDLAGS)" \
		INSTALL_PROG=":"
endef

define Package/n2n_v1/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/n2n_v1/edge $(1)/usr/sbin/edge1
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/n2n_v1/supernode $(1)/usr/sbin/supernode1
	$(INSTALL_DIR) $(1)/etc/config/
	$(INSTALL_DATA) ./files/edge1.config $(1)/etc/config/edge1
	$(INSTALL_DATA) ./files/supernode1.config $(1)/etc/config/supernode1
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/edged1.init $(1)/etc/init.d/edged1
	$(INSTALL_BIN) ./files/supernoded1.init $(1)/etc/init.d/supernoded1
endef

define Package/n2n_v2/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/n2n_v2/edge $(1)/usr/sbin/edge2
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/n2n_v2/supernode $(1)/usr/sbin/supernode2
	$(INSTALL_DIR) $(1)/etc/config/
	$(INSTALL_DATA) ./files/edge2.config $(1)/etc/config/edge2
	$(INSTALL_DATA) ./files/supernode2.config $(1)/etc/config/supernode2
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/edged2.init $(1)/etc/init.d/edged2
	$(INSTALL_BIN) ./files/supernoded2.init $(1)/etc/init.d/supernoded2
endef

define Package/$(PKG_NAME)/conffiles
/etc/config/edge1
/etc/config/supernode1
/etc/config/edge2	
/etc/config/supernode2
endef

$(eval $(call BuildPackage,n2n_v1))
$(eval $(call BuildPackage,n2n_v2))
