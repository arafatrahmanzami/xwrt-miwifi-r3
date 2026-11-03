include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-easy-setup-prebuilt
PKG_VERSION:=2.0.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/luci-app-easy-setup-prebuilt
  SECTION:=luci
  CATEGORY:=LuCI
  SUBMENU:=3. Applications
  TITLE:=Prebuilt LuCI Easy Setup
  DEPENDS:=+luci-compat +luci-base +rpcd +ucode +ucode-mod-fs +ucode-mod-uci +ucode-mod-uloop +lua
endef

define Package/luci-app-easy-setup-prebuilt/description
  Pre-compiled LuCI Easy Setup v2.0.0-r1, extracted from upstream APK.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./files/luci-app-easy-setup-2.0.0-r1.apk $(PKG_BUILD_DIR)/
endef

define Build/Compile
	true
endef

define Package/luci-app-easy-setup-prebuilt/install
	$(INSTALL_DIR) $(1)
	$(STAGING_DIR_HOST)/bin/apk extract --allow-untrusted \
		--destination $(1) $(PKG_BUILD_DIR)/luci-app-easy-setup-2.0.0-r1.apk
	rm -f $(1)/lib/apk/packages/luci-app-easy-setup.list
	rmdir -p $(1)/lib/apk/packages 2>/dev/null || true
	chmod +x $(1)/etc/init.d/easy_setup $(1)/usr/libexec/rpcd/easy_setup 2>/dev/null || true
endef

$(eval $(call BuildPackage,luci-app-easy-setup-prebuilt))
