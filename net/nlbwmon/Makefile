include $(TOPDIR)/rules.mk

PKG_NAME:=nlbwmon
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/jow-/nlbwmon.git
PKG_SOURCE_DATE:=2017-12-05
PKG_SOURCE_VERSION:=75accd647459a8a4167f9baa402d116cad41caa9
PKG_MIRROR_HASH:=821572fdd11bba4a62ecea0b0ddee24645d2ceccdfe7a83dfe5f5edea433ef02

CMAKE_INSTALL:=1

PKG_MAINTAINER:=Jo-Philipp Wich <jo@mein.io>
PKG_LICENSE:=ISC
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS += -DLIBNL_LIBRARY_TINY=ON
TARGET_CFLAGS += -I$(STAGING_DIR)/usr/include/libnl-tiny

define Package/nlbwmon
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libubox +libnl-tiny +zlib +kmod-nf-conntrack-netlink
  TITLE:=LEDE Traffic Usage Monitor
endef

define Package/nlbwmon/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/nlbwmon $(1)/usr/sbin/nlbwmon
	$(LN) nlbwmon $(1)/usr/sbin/nlbw
	$(INSTALL_DIR) $(1)/usr/share/nlbwmon
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/protocols.txt $(1)/usr/share/nlbwmon/protocols
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/nlbwmon.init $(1)/etc/init.d/nlbwmon
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/nlbwmon.config $(1)/etc/config/nlbwmon
endef

define Package/nlbwmon/conffiles
/usr/share/nlbwmon/protocols
endef


$(eval $(call BuildPackage,nlbwmon))
