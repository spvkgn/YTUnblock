# This file is used by OpenWRT SDK buildsystem to package the application for routers.

include $(TOPDIR)/rules.mk

PKG_NAME:=youtubeUnblock
PKG_VERSION:=0.3.0
PKG_REV:=e649ef5567846064f7466786a3c6fc6af4fd18f5
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/Waujito/youtubeUnblock.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/youtubeUnblock
	SECTION:=net
	CATEGORY:=Networking
	TITLE:=youtubeUnblock
	DEPENDS:=+libpthread +libnetfilter-queue
	URL:=https://github.com/Waujito/youtubeUnblock
	MAINTAINER:=Vadim Vetrov <vetrovvd@gmail.com>
endef

define Package/youtubeUnblock/description
	Bypasses Googlevideo detection systems that relies on SNI
endef

define Build/Prepare
        $(Build/Prepare/Default)
	$(Build/Patch)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		USE_SYS_LIBS=yes \
		CROSS_COMPILE_PLATFORM=$(GNU_TARGET_NAME)
endef

define Package/youtubeUnblock/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/build/youtubeUnblock $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/youtubeUnblock.init $(1)/etc/init.d/youtubeUnblock
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/youtubeUnblock.config $(1)/etc/config/youtubeUnblock
endef
# 	$(INSTALL_DIR) $(1)/etc/uci-defaults
# 	$(INSTALL_BIN) ./files/youtubeUnblock.defaults $(1)/etc/uci-defaults
# 	$(INSTALL_DATA) ./files/firewall.include $(1)/etc/firewall.youtubeUnblock

# define Package/youtubeUnblock/prerm
# #!/bin/sh
# f=firewall.youtubeUnblock
# uci get "$$f" >/dev/null || exit 0
# uci batch <<-EOF
# 	delete $$f
# 	commit firewall
# EOF
# endef

$(eval $(call BuildPackage,youtubeUnblock))
