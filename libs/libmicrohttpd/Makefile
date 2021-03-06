#
# Copyright (C) 2010-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libmicrohttpd
PKG_VERSION:=0.9.70
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@GNU/libmicrohttpd
PKG_HASH:=90d0a3d396f96f9bc41eb0f7e8187796049285fabef82604acd4879590977307

PKG_MAINTAINER:=Alexander Couzens <lynxis@fe80.eu>
PKG_LICENSE:=LGPL-2.1-or-later
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libmicrohttpd/default
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=GNU libmicrohttpd is a library that runs an HTTP server.
  URL:=https://www.gnu.org/software/libmicrohttpd/
endef

define Package/libmicrohttpd-no-ssl
$(call Package/libmicrohttpd/default)
  VARIANT:=nossl
  DEFAULT_VARIANT:=1
  PROVIDES:=libmicrohttpd
endef

define Package/libmicrohttpd-ssl
$(call Package/libmicrohttpd/default)
  TITLE+= with SSL support
  VARIANT:=ssl
  DEPENDS:=+libgcrypt +libgnutls +libgpg-error
  PROVIDES:=libmicrohttpd
endef

define Package/libmicrohttpd/description
  GNU libmicrohttpd is a small C library that is supposed to make it easy
  to run an HTTP server as part of another application.
endef

CONFIGURE_ARGS += \
	--disable-curl \
	--disable-rpath \
	--disable-doc \
	--disable-examples \
	--disable-poll \
	--enable-epoll \
	--with-pic

ifeq ($(BUILD_VARIANT),ssl)
CONFIGURE_ARGS += \
	--enable-https \
	--with-gnutls
else
CONFIGURE_ARGS += \
	--disable-https \
	--without-gnutls
endif

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/include/microhttpd.h $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libmicrohttpd.{so*,a,la} $(1)/opt/lib/
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libmicrohttpd.pc $(1)/opt/lib/pkgconfig/
endef

define Package/libmicrohttpd-no-ssl/install
	$(INSTALL_DIR) $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libmicrohttpd.so* $(1)/opt/lib/
endef

define Package/libmicrohttpd-ssl/install
	$(INSTALL_DIR) $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libmicrohttpd.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,libmicrohttpd-no-ssl))
$(eval $(call BuildPackage,libmicrohttpd-ssl))
