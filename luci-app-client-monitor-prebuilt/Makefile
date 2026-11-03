include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-client-monitor-prebuilt
PKG_VERSION:=1.0.0
PKG_RELEASE:=2

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/luci-app-client-monitor-prebuilt
  SECTION:=luci
  CATEGORY:=LuCI
  SUBMENU:=3. Applications
  TITLE:=Prebuilt LuCI Client Monitor
  DEPENDS:=+luci-compat +luci-base +rpcd +ucode +ucode-mod-fs +ucode-mod-uci +ucode-mod-uloop +lua
endef

define Package/luci-app-client-monitor-prebuilt/description
  Pre-compiled LuCI Client Monitor v1.0.0-r2, extracted from upstream APK.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./files/luci-app-client-monitor-1.0.0-r2.apk $(PKG_BUILD_DIR)/
endef

define Build/Compile
	true
endef

define Package/luci-app-client-monitor-prebuilt/install
	$(INSTALL_DIR) $(1)
	$(STAGING_DIR_HOST)/bin/apk extract --allow-untrusted \
		--destination $(1) $(PKG_BUILD_DIR)/luci-app-client-monitor-1.0.0-r2.apk
	rm -f $(1)/lib/apk/packages/luci-app-client-monitor.list
	rmdir -p $(1)/lib/apk/packages 2>/dev/null || true
	chmod +x $(1)/etc/init.d/client_monitor $(1)/usr/sbin/client_monitor_collect $(1)/usr/libexec/rpcd/client_monitor $(1)/usr/bin/ap_monitor 2>/dev/null || true
	chmod +x $(1)/etc/hotplug.d/net/99-client-monitor 2>/dev/null || true
endef

$(eval $(call BuildPackage,luci-app-client-monitor-prebuilt))
