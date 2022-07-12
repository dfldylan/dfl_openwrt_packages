# https://github.com/immortalwrt/luci.git^d1323c38f0a1392b32561a652b714c6390e29614
include $(TOPDIR)/rules.mk

LUCI_TITLE:=LuCI support for UUgamebooster
LUCI_DEPENDS:=+uugamebooster
LUCI_PKGARCH:=all

PKG_NAME:=luci-app-uugamebooster
PKG_RELEASE:=$(COMMITCOUNT)

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
