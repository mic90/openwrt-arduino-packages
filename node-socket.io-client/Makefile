#
# Copyright (C) 2014 Arduino LLC
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NPM_NAME:=socket.io-client
PKG_NAME:=node-$(PKG_NPM_NAME)
PKG_VERSION:=1.4.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NPM_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=http://registry.npmjs.org/$(PKG_NPM_NAME)/-/
PKG_MD5SUM:=7b23768a859c6726ef321b50e67f4cc7

PKG_BUILD_DEPENDS:=node/host
PKG_NODE_VERSION:=6.11.2

include $(INCLUDE_DIR)/package.mk

define Package/node-socket.io-client
  DEPENDS:=+node +node-ws
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Socket.IO client for the browser and node.js
  URL:=https://www.npmjs.org/package/socket.io-client
endef

define Package/node-socket.io-client/description
 Socket.IO client for the browser and node.js
endef

define Build/Prepare
	/bin/tar xzf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR) --strip-components 1
	$(Build/Patch)
endef

define Build/Compile
	$(MAKE_FLAGS) \
	npm_config_arch=$(CONFIG_ARCH) \
	npm_config_nodedir=$(BUILD_DIR)/node-v$(PKG_NODE_VERSION)/ \
	npm_config_cache=$(BUILD_DIR)/node-v$(PKG_NODE_VERSION)/npm-cache \
	PREFIX="$(PKG_INSTALL_DIR)/usr/" \
	npm install --build-from-source --target_arch=$(CPU) -g $(PKG_BUILD_DIR)
endef

define Package/node-socket.io-client/install
	mkdir -p $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/* $(1)/usr/lib/node/
endef

$(eval $(call BuildPackage,node-socket.io-client))

