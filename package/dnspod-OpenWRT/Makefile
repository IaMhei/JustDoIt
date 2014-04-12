#
# Copyright (C) 2010-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dnspod
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/dnspod
   SECTION:=net
   CATEGORY:=Network
   DEPENDS:=+curl
   TITLE:=dnspod client for OpenWRT
   MAINTAINER:=IaMHei <iamhei@qq.com>
   PKGARCH:=all
endef

define Package/dnspod/conffiles
    /etc/config/dnspod
    /etc/cacert.pem
endef

define Build/Compile
endef

define Package/dnspod/install
   $(CP) ./files/* $(1)
endef

define Package/dnspod/postinst
   [ -n "$${IPKG_INSTROOT}" ] || /etc/init.d/dnspod enable
   exit 0
endef

$(eval $(call BuildPackage,dnspod))
