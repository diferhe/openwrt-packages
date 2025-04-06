# SPDX-License-Identifier: Apache-2.0
#
# Copyright (C) 2025 Mateusz Mazelanik <mateusz.mazelanik@gmail.com>

include $(TOPDIR)/rules.mk

PKG_NAME:=blocky
PKG_VERSION:=0.25
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/0xERR0R/blocky/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=856f09cd5df5dc20a44067113dd200a3e74465c3ded2b5dcd473188b3c764b11

PKG_MAINTAINER:=Mateusz Mazelanik <mateusz.mazelanik@gmail.com>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0
PKG_BUILD_FLAGS:=no-mips16

GO_PKG:=github.com/0xERR0R/blocky

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/blocky
  SECTION:=net
  CATEGORY:=Network
  TITLE:=DNS proxy and ad-blocker 
  URL:=https://github.com/0xERR0R/blocky
  DEPENDS:=$(GO_ARCH_DEPENDS)
endef

define Package/blocky/description
  Fast and lightweight DNS proxy as ad-blocker
  for local network with many features
endef

define Package/blocky/conffiles
/etc/config/blocky
/etc/blocky/
endef

define Package/blocky/install
	$(call GoPackage/Package/Install/Bin,$(1))

	$(INSTALL_DIR) $(1)/etc/blocky/
	$(INSTALL_CONF) $(CURDIR)/files/sample_config.yml $(1)/etc/blocky/config.yml
	$(INSTALL_DIR) $(1)/etc/config/
	$(INSTALL_CONF) $(CURDIR)/files/blocky.config $(1)/etc/config/blocky
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) $(CURDIR)/files/blocky.init $(1)/etc/init.d/blocky
endef

$(eval $(call GoBinPackage,blocky))
$(eval $(call BuildPackage,blocky))