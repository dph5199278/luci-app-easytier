include $(TOPDIR)/rules.mk
-include $(dir $(lastword $(MAKEFILE_LIST)))../version.mk

PKG_NAME:=easytier
PKG_VERSION:=$(or $(EASYTIER_VERSION),2.5.0)

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=A simple, decentralized mesh VPN with WireGuard support.
	DEPENDS:=+kmod-tun
	URL:=https://github.com/EasyTier/EasyTier
	MENU:=1
endef

define Package/$(PKG_NAME)/description
  A simple, decentralized mesh VPN with WireGuard support.
endef

define Package/$(PKG_NAME)/config
	config EASYTIER_INCLUDE_WEBCONSOLE
		bool "Include Web Console (easytier-web)"
		depends on PACKAGE_$(PKG_NAME)
		default y
		help
		  Install the easytier-web web console.
endef

define Build/Prepare
	[ ! -f $(PKG_BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION).zip ] && wget https://github.com/dph5199278/EasyTier/actions/runs/23480943607/artifacts/6076475475 -O $(PKG_NAME)-$(PKG_VERSION).zip
	unzip -j $(PKG_NAME)-$(PKG_VERSION).zip -d $(PKG_BUILD_DIR)
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/easytier-core $(1)/usr/bin/easytier-core
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/easytier-cli $(1)/usr/bin/easytier-cli
ifdef CONFIG_EASYTIER_INCLUDE_WEBCONSOLE
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/easytier-web-embed $(1)/usr/bin/easytier-web
endif
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
