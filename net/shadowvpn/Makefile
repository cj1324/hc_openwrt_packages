include $(TOPDIR)/rules.mk

PKG_NAME:=ShadowVPN
PKG_VERSION:=0.1.3
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/cj1324/ShadowVPN.git
PKG_SOURCE_VERSION:=17a6a0cc6c4c0f6169bffe882f39be89ef82f652
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_MAINTAINER:=clowwindy <clowwindy42@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk


define Package/ShadowVPN
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=VPN
  TITLE:=ShadowVPN
  URL:=https://github.com/cj1324/ChinaDNS-OpenWRT
  DEPENDS:=+libsodium +kmod-tun
endef


define Package/ShadowVPN/description
ShadowVPN is a fast, safe VPN based on libsodium. Designed for low end devices
endef

CMAKE_OPTIONS = \
     -DCMAKE_INSTALL_PREFIX=/usr

define Package/ShadowVPN/conffiles
/etc/config/shadowvpn
endef

define Package/ShadowVPN/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/shadowvpn $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/shadowvpn.init $(1)/etc/init.d/shadowvpn
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/shadowvpn.conf $(1)/etc/config/shadowvpn
endef

$(eval $(call BuildPackage,ShadowVPN))
