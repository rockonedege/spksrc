PKG_NAME = libmysqlclient
PKG_VERS = 6.1.11
PKG_EXT = tar.gz
DIST_NAME = mysql-connector-c-$(PKG_VERS)-src
PKG_DIST_NAME = $(DIST_NAME).$(PKG_EXT)
PKG_DIST_SITE = https://cdn.mysql.com/archives/$(PKG_NAME)
PKG_DIR = $(DIST_NAME)

DEPENDS =

HOMEPAGE = https://downloads.mysql.com/archives/c-c
COMMENT  = MySQL C API (libmysqlclient) 
LICENSE  = GNU GPLv2

CONFIGURE_TARGET = mysql-connector-c_configure
PRE_INSTALL_TARGET = mysql-connector-c_pre_install

CMAKE_ARGS = -DCMAKE_BUILD_TYPE=Release
CMAKE_ARGS += -DCMAKE_INSTALL_PREFIX=$(INSTALL_PREFIX)
# MySQL specific:
CMAKE_ARGS += -DSTACK_DIRECTION=1
CMAKE_ARGS += -DWITH_UNIT_TESTS=OFF
CMAKE_ARGS += -DWITH_EMBEDDED_SERVER=FALSE
CMAKE_ARGS += -DDEFAULT_CHARSET=utf8 -DDEFAULT_COLLATION=utf8_general_ci
# Fix full lib version:
CMAKE_ARGS += -DSHARED_LIB_PATCH_VERSION=0


include ../../mk/spksrc.native-cc.mk

.PHONY: mysql-connector-c_configure
mysql-connector-c_configure:
	$(RUN) cmake $(CMAKE_ARGS) .

.PHONY: mysql-connector-c_pre_install
mysql-connector-c_pre_install:
	$(RUN) install -m 755 -d $(INSTALL_DIR)$(INSTALL_PREFIX)/bin/
	$(RUN) cp $(WORK_DIR)/$(PKG_DIR)/extra/comp_err $(INSTALL_DIR)$(INSTALL_PREFIX)/bin/
