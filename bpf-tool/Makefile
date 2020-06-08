include $(TOPDIR)/rules.mk

PKG_NAME:=bpf-tool
PKG_LICENSE:=GPL-2.0
PKG_MAINTAINER:=Tiffany Kalin <tkalin@untangle.com>

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Netronome/bpf-tool.git
PKG_HASH:=96d6c0a9bc94a7c01e07d9edc1b71c8c134d43bc

PKG_VERSION:=v0.1.0
PKG_SOURCE_VERSION:=0.1.0
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2

include $(INCLUDE_DIR)/package.mk

define Package/bpf-tool
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Firewall
  TITLE:=Userspace bpf-tool
  URL:=https://github.com/Netronome/bpf-tool.git
  DEPENDS:=+libelf +libbpf +libbfd +libopcodes
  KCONFIG:=CONFIG_BPF=y CONFIG_BPF_SYSCALL=y \
	   CONFIG_BPF_JIT=y CONFIG_HAVE_EBPF_JIT=y 
endef

define Package/bpf-tool/description
	Userspace bpf-tool
endef

define Package/bpf-tool/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bpf-tool $(1)/usr/bin/bpf-tool
endef

$(eval $(call BuildPackage,bpf-tool))
