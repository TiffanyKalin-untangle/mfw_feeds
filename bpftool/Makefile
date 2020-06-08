include $(TOPDIR)/rules.mk

PKG_NAME:=bpftool
PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=Sebastien Delafond <sdelafond@gmail.com>
PKG_VERSION:=0.0.1
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Netronome/bpf-tool.git
PKG_HASH:=96d6c0a9bc94a7c01e07d9edc1b71c8c134d43bc

include $(INCLUDE_DIR)/package.mk

define Package/bpftool
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Firewall
  TITLE:=Userspace bpftool
  DEPENDS:=+libelf +libbpf +libbfd +libopcodes
  KCONFIG:=
endef

define Package/bpftool/description
	Userspace bpftool
endef

define Package/bpftool/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bpftool $(1)/usr/bin/bpftool
endef

$(eval $(call BuildPackage,bpftool))
