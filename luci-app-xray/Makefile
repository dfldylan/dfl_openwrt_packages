# https://github.com/yichya/luci-app-xray.git^4b0969a2d0f04ccdee1f395bacc427767b7e2704
#
# Copyright 2020 Xingwang Liao <kuoruan@gmail.com>
# Licensed to the public under the MIT License.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-xray
PKG_VERSION:=1.0.2
PKG_RELEASE:=0

PKG_LICENSE:=MIT
PKG_MAINTAINER:=BI7PRK

LUCI_TITLE:=LuCI support for xray-core and v2ray-core
LUCI_DEPENDS:=+jshn +ip +ipset +iptables +iptables-mod-tproxy +resolveip +dnsmasq-full
LUCI_PKGARCH:=all

define Package/$(PKG_NAME)/conffiles
/etc/config/xray
/etc/xray/transport.json
/etc/xray/directlist.txt
/etc/xray/proxylist.txt
endef

include $(TOPDIR)/feeds/luci/luci.mk

define Package/$(PKG_NAME)/postinst
#!/bin/sh

if [ -z "$${IPKG_INSTROOT}" ] ; then
	( . /etc/uci-defaults/40_luci-xray ) && rm -f /etc/uci-defaults/40_luci-xray

	rm -rf /tmp/luci-indexcache /tmp/luci-modulecache/

	killall -HUP rpcd 2>/dev/null
fi

chmod 755 "/etc/init.d/xray" >/dev/null 2>&1

ln -sf "/init.d/xray"  "/etc/rc.d/S99xray" >/dev/null 2>&1

exit 0
endef

define Package/$(PKG_NAME)/postrm
#!/bin/sh

if [ -s "/etc/rc.d/S99xray" ] ; then
	rm -f "/etc/rc.d/S99xray"
fi

if [ -z "$${IPKG_INSTROOT}" ] ; then
	rm -rf /tmp/luci-indexcache /tmp/luci-modulecache/
fi

exit 0
endef

# call BuildPackage - OpenWrt buildroot signature
