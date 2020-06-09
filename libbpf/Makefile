include $(TOPDIR)/rules.mk

PKG_NAME:=libbpf
PKG_VERSION:=1.0.4

PKG_MAINTAINER:=Tiffany Kalin <tkalin@untangle.com>

PKG_LICENSE:=LGPL-2.1+

include $(INCLUDE_DIR)/package.mk

define Package/libbpf
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Libbpf
  DEPENDS:=+libelf1
endef

define Package/libbpf/description
*ADD DESCRIPTION*
endef

CONFIGURE_ARGS+= \
	--enable-shared \
	--enable-static \

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libbpf $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libbpf.{a,so*} $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libbpf.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libbpf/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libbpf.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libbpf))
