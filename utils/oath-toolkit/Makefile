include $(TOPDIR)/rules.mk

PKG_NAME:=oath-toolkit
PKG_VERSION:=2.6.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://git.sv.gnu.org/oath-toolkit.git
PKG_SOURCE_VERSION:=e00eed8a8c77b2f7ab50212fb5b1453264341c95
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)

PKG_MAINTAINER:=HanChen <chen1324@gmail.com>
PKG_LICENSE:=GPL-3.0+


include $(INCLUDE_DIR)/package.mk

define Package/oath-toolkit
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+libxml2
	TITLE:=The OATH Toolkit makes it easy to build one-time password authentication systems.
	URL:=https://savannah.nongnu.org/projects/oath-toolkit/
endef

define Package/oath-toolkit/description
  The OATH Toolkit makes it easy to build one-time password authentication systems.
  It contains a shared library, a command line tool and a PAM module.
  Supported technologies include the event-based HOTP algorithm (RFC4226) and the time-based TOTP algorithm (RFC6238).
  OATH stands for Open AuTHentication, which is the organization that specify the algorithms.
endef

define Build/Prepare
	$(PKG_UNPACK)
	cd $(PKG_BUILD_DIR) && rm -f cfg.mk
	cd $(PKG_BUILD_DIR) && printf "gdoc_MANS =\ngdoc_TEXINFOS =\n" > liboath/man/Makefile.gdoc
	cd $(PKG_BUILD_DIR) && printf "gdoc_MANS =\ngdoc_TEXINFOS =\n" > libpskc/man/Makefile.gdoc
	cd $(PKG_BUILD_DIR) && touch ChangeLog
	cd $(PKG_BUILD_DIR) && autoreconf --force --install
endef

define Build/Configure
	$(call Build/Configure/Default,--disable-pam --disable-pskc)
endef

define Package/oath-toolkit/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/oathtool/.libs/oathtool $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/liboath/.libs/liboath.{a,so*} $(1)/usr/lib/
endef

$(eval $(call BuildPackage,oath-toolkit))
