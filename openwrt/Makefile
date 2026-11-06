include $(TOPDIR)/rules.mk

PKG_NAME:=far2l
# Версия будет подставлена из workflow (например, дата или тег)
PKG_VERSION:=@VERSION@
PKG_RELEASE:=1
PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=LICENSE.txt

# Указываем URL на ваш форк, чтобы собиралась именно ваша версия кода
PKG_SOURCE_URL:=https://github.com/ВАШ_ЛОГИН/far2l/archive/
PKG_SOURCE:=$(PKG_VERSION).tar.gz
# Хеш можно не указывать (skip) для CI-сборок, но для воспроизводимости лучше вычислять
PKG_HASH:=skip
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_PARALLEL:=1

CMAKE_INSTALL:=1
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/far2l/Default
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=FAR Manager v2 (Linux port)
  URL:=https://github.com/elfmz/far2l
endef

define Package/far2l
  $(call Package/far2l/Default)
  DEPENDS:=+libstdcpp +libarchive-noopenssl
  VARIANT:=default
endef

define Package/far2l-tiny
  $(call Package/far2l/Default)
  TITLE+= (minimal)
  DEPENDS:=+libstdcpp
  VARIANT:=tiny
endef

define Package/far2l-full
  $(call Package/far2l/Default)
  TITLE+= (full)
  DEPENDS:=+libstdcpp +libarchive-noopenssl +libneon +libssh +libxml2
  VARIANT:=full
endef

define Package/far2l/description
  Linux port of FAR Manager v2.
endef

define Package/far2l-tiny/description
  $(call Package/far2l/description)
  Build with no plugins, only English language.
endef

define Package/far2l-full/description
  $(call Package/far2l/description)
  Build with Colorer and NetRocks plugins.
endef

define Package/far2l/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/usr/lib/far2l $(1)/usr/share/far2l
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/far2l $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/far2l/* $(1)/usr/lib/far2l/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/far2l/* $(1)/usr/share/far2l/
	$(RM) -rf $(1)/usr/lib/far2l/themes
	$(RM) -rf $(1)/usr/share/far2l/themes/CMakeFiles
endef

define Package/far2l-tiny/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/usr/share/far2l
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/far2l $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/share/far2l/FarEng.* $(1)/usr/share/far2l/
	$(CP) $(PKG_INSTALL_DIR)/usr/share/far2l/*.{sh,ini} $(1)/usr/share/far2l/
endef

define Package/far2l-full/install
	$(call Package/far2l/install,$1)
	$(RM) -rf $(1)/usr/lib/far2l/themes
	$(RM) -rf $(1)/usr/share/far2l/themes/CMakeFiles
endef

# Отключаем необязательные компоненты, которые могут усложнить сборку на роутере
CMAKE_OPTIONS += \
	-DADB=no \
	-DARCLITE=no \
	-DIMAGEVIEWER=no \
	-DOPENWITH=no \
	-DUSEUCD=no \
	-DUSEWX=no \
	-DGIT_DATE=@GIT_DATE@ \
	-DGIT_HASH=@GIT_HASH@ \
	-DCMAKE_DISABLE_FIND_PACKAGE_Git=ON

ifeq ($(BUILD_VARIANT),default)
  CMAKE_OPTIONS += -DCOLORER=no -DNETROCKS=no
else ifeq ($(BUILD_VARIANT),tiny)
  CMAKE_OPTIONS += -DFAR2MACRO=no
endif

$(eval $(call BuildPackage,far2l))
$(eval $(call BuildPackage,far2l-tiny))
$(eval $(call BuildPackage,far2l-full))
