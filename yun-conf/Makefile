#
# Copyright (c) 2013 Arduino LLC. All right reserved.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=yun-conf
PKG_VERSION:=1.2.0
PKG_RELEASE:=5

include $(INCLUDE_DIR)/package.mk

define Package/yun-conf
  SECTION:=utils
  CATEGORY:=Base system
  TITLE:=Custom Yún configurations
  DEPENDS:=+avahi-dbus-daemon +base-files
endef

define Package/yun-conf/conffiles
/etc/avahi/services/arduino.service
/etc/config/arduino
/etc/httpd.conf
endef

define Build/Compile
	# NOOP
endef

define Package/yun-conf/install
	$(INSTALL_DIR) $(1)/etc/avahi/services
	$(INSTALL_DIR) $(1)/etc/arduino
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DIR) $(1)/etc/hotplug.d/button
	$(INSTALL_DIR) $(1)/etc/opkg/keys
	$(INSTALL_DIR) $(1)/www/cgi-bin

	$(INSTALL_DATA) ./files/etc/avahi/services/arduino.service $(1)/etc/avahi/services/
	$(INSTALL_DATA) ./files/etc/hotplug.d/button/buttons $(1)/etc/hotplug.d/button/

	$(INSTALL_DATA) ./files/etc/httpd.conf $(1)/etc/
	$(INSTALL_DATA) ./files/etc/config/arduino $(1)/etc/config/

	$(INSTALL_CONF) ./files/etc/opkg/keys/* $(1)/etc/opkg/keys/

	$(INSTALL_DATA) ./files/etc/arduino/Caterina2-Yun.hex $(1)/etc/arduino/
	$(INSTALL_CONF) ./files/etc/arduino/openwrt-yun-release $(1)/etc/arduino/
	sed -i "s/DATE/`date`/g" $(1)/etc/arduino/openwrt-yun-release
	$(INSTALL_CONF) ./files/etc/arduino/gpg_gen_key_batch $(1)/etc/arduino/
	$(INSTALL_DATA) ./files/etc/arduino/wifi_timezones.csv.gz $(1)/etc/arduino
	$(INSTALL_DATA) ./files/etc/arduino/wifi_error_statuses.csv.gz $(1)/etc/arduino
	$(INSTALL_DATA) ./files/etc/arduino/wifi_error_reasons.csv.gz $(1)/etc/arduino

	$(INSTALL_BIN) ./files/www/cgi-bin/firstconfig.cgi $(1)/www/cgi-bin/
endef

$(eval $(call BuildPackage,yun-conf))
