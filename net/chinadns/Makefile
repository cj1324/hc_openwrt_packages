include $(TOPDIR)/rules.mk

PKG_NAME:=ChinaDNS-OpenWRT
PKG_VERSION:=1.1.3
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/cj1324/ChinaDNS-OpenWRT.git
PKG_SOURCE_VERSION:=e9989517b5604314c8a398eada476e8cfb7b6b1f
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_MAINTAINER:=clowwindy <clowwindy42@gmail.com>

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk


define Package/ChinaDNS-OpenWRT/Default
  SECTION:=net
  CATEGORY:=Network
  TITLE:=ChinaDNS-OpenWRT
  URL:=https://github.com/cj1324/ChinaDNS-OpenWRT
  DEPENDS:=+libuci
endef

define Package/ChinaDNS-OpenWRT
  $(call Package/ChinaDNS-OpenWRT/Default)
endef

define Package/ChinaDNS-OpenWRT/description
A DNS forwarder that ignores incorrect(you knew it) responses. (without chnroute)
endef

CMAKE_OPTIONS = \
     -DCMAKE_INSTALL_PREFIX=/usr \
     -DWITH_UCI:BOOL=ON \
     -DWITH_CHN_ROUTE:BOOL=OFF \
     -DWITH_DEBUG:BOOL=OFF \

define Package/ChinaDNS-OpenWRT/conffiles
/etc/config/chinadns
endef

define Package/ChinaDNS-OpenWRT/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/chinadns $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/chinadns.init $(1)/etc/init.d/chinadns
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/chinadns.conf $(1)/etc/config/chinadns
endef

$(eval $(call BuildPackage,ChinaDNS-OpenWRT))
