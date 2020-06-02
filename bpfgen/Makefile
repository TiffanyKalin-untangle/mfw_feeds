include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=bpfgen 
PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=Sebastien Delafond <sdelafond@gmail.com>
PKG_VERSION:=0.0.1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/kernel-defaults.mk

define Package/bpfgen
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Firewall
  TITLE:=Userspace bpf generator 
  FILES:=$(PKG_BUILD_DIR)/bpfgen
  DEPENDS:=+libnftnl +libmnl
  KCONFIG:=
endef 

define Package/bpfgen/description
	Userspace bpf generator 
endef 

define Build/Compile 
	$(KERNEL_MAKE) SUBDIRS="$(PKG_BUILD_DIR)"
endef 

$(eval $(call BuildPackage,bpfgen))
