include $(TOPDIR)/rules.mk

PKG_NAME:=far2l
PKG_RELEASE:=1
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=LICENSE.txt

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ТВОЙ_ЛОГИН/far2l.git
PKG_SOURCE_VERSION:=master
PKG_MIRROR_HASH:=skip
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_BUILD_PARALLEL:=1

CMAKE_INSTALL:=1
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/far2l
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=FAR Manager v2 (Linux port, console)
  URL:=https://github.com/elfmz/far2l
  DEPENDS:=+libstdcpp +libarchive-noopenssl
endef

define Package/far2l/description
  Linux port of FAR Manager v2, console (TTY) backend only.
endef

define Package/far2l/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/usr/lib/far2l $(1)/usr/share/far2l
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/far2l $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/far2l/* $(1)/usr/lib/far2l/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/far2l/* $(1)/usr/share/far2l/
endef

CMAKE_OPTIONS += \
	-DUSEWX=no \
	-DUSESDL=no \
	-DTTYX=no \
	-DTTYXI=no \
	-DUSEUCD=no \
	-DCOLORER=no \
	-DNETROCKS=no \
	-DADB=no \
	-DALIGN=no \
	-DARCLITE=no \
	-DAUTOWRAP=no \
	-DCALC=no \
	-DIMAGEVIEWER=no \
	-DOPENWITH=no \
	-DFAR2MACRO=OFF \
	-DUNRAR=NO \
	-DCMAKE_DISABLE_FIND_PACKAGE_Git=ON \
	-DCMAKE_BUILD_TYPE=Release

$(eval $(call BuildPackage,far2l))
