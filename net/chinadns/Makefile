include $(TOPDIR)/rules.mk

PKG_NAME:=ChinaDNS-OpenWRT
PKG_VERSION:=1.1.2
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/cj1324/ChinaDNS-OpenWRT.git
PKG_SOURCE_VERSION:=ee6f0f837bf7b2e1b406ddc3ce5df539fd8a2711

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
A DNS forwarder that ignores incorrect(you knew it) responses.
endef

CMAKE_OPTIONS = \
     -DCMAKE_INSTALL_PREFIX=/usr \
     -DWITH_DEBUG=OFF \

define Package/ChinaDNS-OpenWRT/conffiles
/etc/chinadns_iplist.txt
/etc/config/chinadns
endef

define Package/ChinaDNS-OpenWRT/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_CONF) ../iplist.txt $(1)/etc/chinadns_iplist.txt
	$(INSTALL_BIN) ./files/chinadns.init $(1)/etc/init.d/chinadns
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_BIN) ../chinadns.conf $(1)/etc/config/chinadns
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/chinadns $(1)/usr/bin
endef

$(eval $(call BuildPackage,ChinaDNS-OpenWRT))
