include $(TOPDIR)/rules.mk

PKG_NAME:=shadowsocks-libev
PKG_VERSION:=1.4.6
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_URL:=https://github.com/madeye/shadowsocks-libev/archive
PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_MAINTAINER:=Max Lv <max.c.lv@gmail.com>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf
PKG_USE_MIPS16:=0
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/shadowsocks-libev/Default
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Lightweight Secured Socks5 Proxy via ss-redir
  URL:=https://github.com/madeye/shadowsocks-libev
  DEPENDS:= +kmod-ipt-ipset +iptables-mod-nat-extra +ipset
endef

define Package/shadowsocks-libev
  $(call Package/shadowsocks-libev/Default)
  TITLE+= (OpenSSL) [h]
  VARIANT:=openssl
  DEPENDS+= +libopenssl
endef

define Package/shadowsocks-libev-polarssl
  $(call Package/shadowsocks-libev/Default)
  TITLE+= (PolarSSL) [h]
  VARIANT:=polarssl
  DEPENDS+= +libpolarssl
endef

define Package/shadowsocks-libev/description
Shadowsocks-libev is a lightweight secured scoks5 proxy for embedded devices and low end boxes. include ss-tunnel ss-redir.
endef

Package/shadowsocks-libev-polarssl/description=$(Package/shadowsocks-libev/description)

define Package/shadowsocks-libev/conffiles
/etc/config/ssredir.conf
endef

ifeq ($(BUILD_VARIANT),polarssl)
	CONFIGURE_ARGS += --with-crypto-library=polarssl
endif

define Package/shadowsocks-libev/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/etc/init.d $(1)/etc/config
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/ss-redir $(1)/usr/bin/ssredir
	$(INSTALL_BIN) ./files/ssredir.init $(1)/etc/init.d/ssredir
	$(INSTALL_CONF) ./files/ssredir.conf $(1)/etc/config/ssredir
	$(INSTALL_DIR) $(1)/etc/hotplug.d/iface
	$(INSTALL_DATA) ./files/ssredir.hotplug $(1)/etc/hotplug.d/iface/30-ssredir
endef

Package/shadowsocks-libev-polarssl/install=$(Package/shadowsocks-libev/install)

$(eval $(call BuildPackage,shadowsocks-libev))
$(eval $(call BuildPackage,shadowsocks-libev-polarssl))
