include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=bpftool
PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=Sebastien Delafond <sdelafond@gmail.com>
PKG_VERSION:=0.0.1

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/bpftool
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Firewall
  TITLE:=Userspace bpftool
  DEPENDS:=+libelf +libbpf
  KCONFIG:=
endef

include $(INCLUDE_DIR)/kernel-defaults.mk

define Package/bpftool/description
	Userspace bpftool
endef

define Build/Compile 
	$(KERNEL_MAKE) SUBDIRS="$(PKG_BUILD_DIR)"
endef

define Package/bpftool/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/bpftool $(1)/usr/bin/bpftool
endef

$(eval $(call KernelPackage,bpftool))
