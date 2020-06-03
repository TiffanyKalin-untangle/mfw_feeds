include $(TOPDIR)/rules.mk

PKG_NAME:=bpfgen
PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=Sebastien Delafond <sdelafond@gmail.com>
PKG_VERSION:=0.0.1

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/bpfgen
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Firewall
  TITLE:=Userspace bpf generator
  DEPENDS:=+libnftnl +libmnl +jansson
  KCONFIG:=
endef

define Package/bpfgen/description
	Userspace bpf generator
endef

define Package/bpfgen/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/bpfgen $(1)/usr/bin/bpfgen
endef

$(eval $(call BuildPackage,bpfgen))
