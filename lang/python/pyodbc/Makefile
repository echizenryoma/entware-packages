# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pyodbc
PKG_VERSION:=4.0.26
PKG_RELEASE:=3

PYPI_NAME:=$(PKG_NAME)
PKG_HASH:=e52700b5d24a846483b5ab80acd9153f8e593999c9184ffea11596288fb33de3
PKG_BUILD_DEPENDS:=python3 unixodbc
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE.txt
PKG_MAINTAINER:=Daniel Golle <daniel@makrotopia.org>

PKG_BUILD_DEPENDS:=unixodbc/host

include ../pypi.mk
include $(INCLUDE_DIR)/package.mk
include ../python3-package.mk

define Package/python3-pyodbc
  SECTION:=lang
  CATEGORY:=Languages
  SUBMENU:=Python
  TITLE:=python3-pyodbc
  URL:=https://github.com/mkleehammer/pyodbc
  DEPENDS:=+unixodbc +python3-light +libstdcpp
endef

define Package/python3-pyodbc/description
DB API Module for ODBC

A Python DB API 2 module for ODBC. This project provides an up-to-date,
convenient interface to ODBC using native data types like datetime and decimal.
endef

$(eval $(call Py3Package,python3-pyodbc))
$(eval $(call BuildPackage,python3-pyodbc))
