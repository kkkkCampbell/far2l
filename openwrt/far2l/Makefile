include $(TOPDIR)/rules.mk

PKG_NAME:=far2l
PKG_VERSION:=main
PKG_RELEASE:=1
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=LICENSE.txt

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ТВОЙ_ЛОГИН/far2l.git
PKG_SOURCE_VERSION:=main
PKG_MIRROR_HASH:=skip
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_BUILD_PARALLEL:=1

CMAKE_INSTALL:=1
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/far2l
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=FAR Manager v2 (Linux port)
  URL:=https://github.com/elfmz/far2l
  DEPENDS:=+libstdcpp +libarchive-noopenssl
endef

define Package/far2l/description
  Linux port of FAR Manager v2.
endef

define Package/far2l/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/usr/lib/far2l $(1)/usr/share/far2l
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/far2l $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/far2l/* $(1)/usr/lib/far2l/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/far2l/* $(1)/usr/share/far2l/
endef

CMAKE_OPTIONS += \
	-DADB=no \
	-DARCLITE=no \
	-DIMAGEVIEWER=no \
	-DOPENWITH=no \
	-DUSEUCD=no \
	-DUSEWX=no \
	-DCOLORER=no \
	-DNETROCKS=no \
	-DCMAKE_DISABLE_FIND_PACKAGE_Git=ON

$(eval $(call BuildPackage,far2l))
