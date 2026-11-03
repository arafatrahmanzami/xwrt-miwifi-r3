include $(TOPDIR)/rules.mk

PKG_NAME:=openlink-portal
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/openlink-portal
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Captive Portals
  TITLE:=OpenLink Captive Portal
  DEPENDS:=+nodogsplash +libpthread
endef

define Package/openlink-portal/description
  OpenLink Captive Portal with Go backend and web frontend.
  Run /root/setup.sh after flashing.
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./backend/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	cd $(PKG_BUILD_DIR) && \
	GOOS=linux GOARCH=mipsle GOMIPS=softfloat CGO_ENABLED=0 \
	go build -ldflags="-s -w" -o voucher_server .
endef

define Package/openlink-portal/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/voucher_server $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/openlink-portal
	$(CP) ./files/* $(1)/etc/openlink-portal/

	$(INSTALL_DIR) $(1)/root
	$(INSTALL_BIN) ./files/setup.sh $(1)/root/setup.sh
endef

$(eval $(call BuildPackage,openlink-portal))
