# New ports collection makefile for:	bsdinstaller
# Date created:			July 24, 2005
# Whom:				Chris Pressey <cpressey@catseye.mine.nu>

PORTNAME=	bsdinstaller
PORTVERSION=    2.0
INTERNAL=	YES
CATEGORIES=	sysutils
DISTNAME=	${PORTNAME}-${PORTVERSION}
WRKSRC=		work/installer/src

.if defined(WITH_NLS)
LIB_DEPENDS=	intl.9:${PORTSDIR}/devel/gettext
.endif

MAINTAINER=	cpressey@catseye.mine.nu
COMMENT=	BSD Installer mega-package

# XXX Not sure if this should be LOCALBASE or PREFIX... probably LOCALBASE?
.if defined(WITH_NLS)
LOCALEDIR=	${LOCALBASE}/share/locale
LANGUAGES=	ru
ALL_TARGET=	nls
.else
MAKE_ARGS+=	LOCALEDIR="" NLS_CFLAGS="" NLS_LDFLAGS=""
.endif

.if defined(WITH_QT)
USE_QT_VER=	3
.endif

DFUIBE_LUA_DIR=	${PREFIX}/share/dfuibe_lua

# Make it so that we don't have to build the parts we're not installing...
.if defined(WITH_QT)
MAKE_ARGS+= BUILD_QT_FRONTEND=true
.else
MAKE_ARGS+= BUILD_QT_FRONTEND=false
.endif

.if defined(WITH_CGI)
MAKE_ARGS+= BUILD_CGI_FRONTEND=true
.else
MAKE_ARGS+= BUILD_CGI_FRONTEND=false
.endif

.if defined(WITH_CURSES)
MAKE_ARGS+= BUILD_NCURSES_FRONTEND=true
.else
MAKE_ARGS+= BUILD_NCURSES_FRONTEND=false
.endif

.if defined(WITH_C_BACKEND)
MAKE_ARGS+= BUILD_C_BACKEND=true
.else
MAKE_ARGS+= BUILD_C_BACKEND=false
.endif

.if defined(WITH_LUA_BACKEND)
MAKE_ARGS+= BUILD_LUA_BACKEND=true
.else
MAKE_ARGS+= BUILD_LUA_BACKEND=false
.endif

# Don't strip executables if this is being built as a "debuggable" package.
.if defined(DEBUG) || defined(WITH_DEBUG) || defined(WITH_DEBUG_INFO) || defined(EXTRA_CFLAGS)
STRIP=
.endif

###### Packing list.
PLIST_FILES=

# libaura
PLIST_FILES+=	lib/libaura.a			\
		lib/libaura.so			\
		lib/libaura.so.3		\
		include/aura/buffer.h		\
		include/aura/dict.h		\
		include/aura/fspred.h		\
		include/aura/popen.h		\
		include/aura/mem.h

# libdfui
PLIST_FILES+=	lib/libdfui.a			\
		lib/libdfui.so			\
		lib/libdfui.so.4		\
		include/dfui/dfui.h		\
		include/dfui/dump.h		\
		include/dfui/lang.h		\
		include/dfui/system.h

# libinstaller
.if defined(WITH_C_BACKEND)
PLIST_FILES+=	lib/libinstaller.a		\
		lib/libinstaller.so		\
		lib/libinstaller.so.5		\
		include/installer/commands.h	\
		include/installer/confed.h	\
		include/installer/diskutil.h	\
		include/installer/functions.h	\
		include/installer/package.h	\
		include/installer/uiutil.h
.endif

# dfuife_curses
.if defined(WITH_CURSES)
PLIST_FILES+=	sbin/dfuife_curses	\
		share/dfuife_curses/fred.txt
.if defined(WITH_NLS)
PLIST_FILES+=	share/locale/ru/LC_MESSAGES/dfuife_curses.mo
.endif
.endif

# dfuife_cgi
.if defined(WITH_CGI)
PLIST_FILES+=	www/dfuife.cgi		\
		www/dfly-pg.gif		\
		www/fred-bg.gif		\
		www/fred.png		\
		www/dfuife.css		\
		www/dfuife.js		\
		www/index.html
.endif

# dfuife_qt
.if defined(WITH_QT)
PLIST_FILES+=	sbin/dfuife_qt
.endif

# dfuibe_installer
.if defined(WITH_C_BACKEND)
PLIST_FILES+=	sbin/dfuibe_installer \
		share/dfuibe_installer/cmdnames.conf
.if defined(WITH_NLS)
PLIST_FILES+=	share/locale/ru/LC_MESSAGES/dfuibe_installer.mo
.endif
.endif

# lua50 - maybe should go into libexec.
.if defined(WITH_LUA_BACKEND)
PLIST_FILES+=	lib/liblua50.so		\
		lib/liblualib50.so	\
		bin/lua50		\
		bin/lua50c

# lua50-compat5.1
PLIST_FILES+=	share/lua/5.0/compat-5.1.lua		\
		lib/lua/${DISTNAME}/compat-5.1.c	\
		lib/lua/${DISTNAME}/compat-5.1.h	\
		bin/lua50c51

# lua50-pty
PLIST_FILES+=	lib/lua/5.0/lpty.so \
		share/lua/5.0/pty.lua

# lua50-app
PLIST_FILES+=	share/lua/5.0/app.lua

# lua50-gettext
.if defined(WITH_NLS)
PLIST_FILES+=	lib/lua/5.0/lgettext.so \
		share/lua/5.0/gettext.lua
.endif

# lua50-filename
PLIST_FILES+=	share/lua/5.0/filename.lua

# lua50-posix
PLIST_FILES+=	lib/lua/5.0/lposix.so	\
		share/lua/5.0/posix.lua

# lua50-dfui
PLIST_FILES+=	lib/lua/5.0/ldfui.so \
		share/lua/5.0/dfui.lua

# lua50-luasocket
PLIST_FILES+=	lib/lua/5.0/lsocket.so		\
		lib/lua/5.0/lmime.so		\
		share/lua/5.0/ftp.lua		\
		share/lua/5.0/http.lua		\
		share/lua/5.0/ltn12.lua		\
		share/lua/5.0/mime.lua		\
		share/lua/5.0/smtp.lua		\
		share/lua/5.0/socket.lua	\
		share/lua/5.0/tp.lua		\
		share/lua/5.0/url.lua

# lua50-transceiver
PLIST_FILES+=	share/lua/5.0/transceiver.lua

# lua50-curses
.if defined(WITH_CURSES)
PLIST_FILES+=	lib/lua/5.0/lcurses.so \
		share/lua/5.0/curses.lua
.endif

# dfuibe_lua
PLIST_FILES+=	share/dfuibe_lua/main.lua \
		share/dfuibe_lua/200_install.lua \
		share/dfuibe_lua/400_configure.lua \
		share/dfuibe_lua/600_upgrade.lua \
		share/dfuibe_lua/800_netboot.lua \
		share/dfuibe_lua/950_reboot.lua \
		share/dfuibe_lua/lib/bitwise.lua \
		share/dfuibe_lua/lib/cmdchain.lua \
		share/dfuibe_lua/lib/configvars.lua \
		share/dfuibe_lua/lib/flow.lua \
		share/dfuibe_lua/lib/menu.lua \
		share/dfuibe_lua/lib/network.lua \
		share/dfuibe_lua/lib/network_ui.lua \
		share/dfuibe_lua/lib/Package.lua \
		share/dfuibe_lua/lib/package_ui.lua \
		share/dfuibe_lua/lib/storage.lua \
		share/dfuibe_lua/lib/storage_ui.lua \
		share/dfuibe_lua/lib/target_system.lua \
		share/dfuibe_lua/lib/target_system_ui.lua \
		share/dfuibe_lua/lib/uinav.lua \
		share/dfuibe_lua/conf/BSDInstaller.lua \
		share/dfuibe_lua/conf/DragonFly.lua \
		share/dfuibe_lua/conf/FreeBSD.lua \
		share/dfuibe_lua/conf/NetBSD.lua \
		share/dfuibe_lua/conf/OpenBSD.lua \
		share/dfuibe_lua/pit/main.lua \
		share/dfuibe_lua/pit/050_welcome.lua \
		share/dfuibe_lua/pit/100_select_language.lua \
		share/dfuibe_lua/pit/150_configure_console.lua \
		share/dfuibe_lua/pit/400_load_kernel_modules.lua \
		share/dfuibe_lua/pit/800_configure_network.lua \
		share/dfuibe_lua/install/main.lua \
		share/dfuibe_lua/install/100_welcome.lua \
		share/dfuibe_lua/install/200_select_disk.lua \
		share/dfuibe_lua/install/220_format_disk.lua \
		share/dfuibe_lua/install/250_partition_disk.lua \
		share/dfuibe_lua/install/270_install_bootblocks.lua \
		share/dfuibe_lua/install/300_select_part.lua \
		share/dfuibe_lua/install/400_select_subparts.lua \
		share/dfuibe_lua/install/405_warn_omitted_subparts.lua \
		share/dfuibe_lua/install/407_create_subparts.lua \
		share/dfuibe_lua/install/410_select_additional_filesystems.lua \
		share/dfuibe_lua/install/420_preselect_packages.lua \
		share/dfuibe_lua/install/450_select_packages.lua \
		share/dfuibe_lua/install/490_confirm_install_os.lua \
		share/dfuibe_lua/install/500_install_os.lua \
		share/dfuibe_lua/install/800_finished.lua \
		share/dfuibe_lua/install/900_reboot.lua \
		share/dfuibe_lua/configure/main.lua \
		share/dfuibe_lua/configure/100_choose_where_from.lua \
		share/dfuibe_lua/configure/200_select_disk.lua \
		share/dfuibe_lua/configure/300_select_part.lua \
		share/dfuibe_lua/configure/400_mount_target_system.lua \
		share/dfuibe_lua/configure/450_init_configuration.lua \
		share/dfuibe_lua/configure/500_menu.lua \
		share/dfuibe_lua/configure/550_write_configuration.lua \
		share/dfuibe_lua/configure/600_unmount_target_system.lua \
		share/dfuibe_lua/configure/menu/main.lua \
		share/dfuibe_lua/configure/menu/100_set_root_password.lua \
		share/dfuibe_lua/configure/menu/200_add_user.lua \
		share/dfuibe_lua/configure/menu/300_set_timezone.lua \
		share/dfuibe_lua/configure/menu/350_set_datetime.lua \
		share/dfuibe_lua/configure/menu/400_change_console_settings.lua \
		share/dfuibe_lua/configure/menu/500_install_packages.lua \
		share/dfuibe_lua/configure/menu/550_remove_packages.lua \
		share/dfuibe_lua/upgrade/main.lua \
		share/dfuibe_lua/upgrade/100_begin_upgrade.lua \
		share/dfuibe_lua/upgrade/200_select_disk.lua \
		share/dfuibe_lua/upgrade/300_select_part.lua \
		share/dfuibe_lua/upgrade/400_mount_target_system.lua \
		share/dfuibe_lua/upgrade/500_perform_upgrade.lua \
		share/dfuibe_lua/upgrade/550_upgrade_configuration.lua \
		share/dfuibe_lua/upgrade/600_unmount_target_system.lua \
		share/dfuibe_lua/netboot/main.lua \
		share/dfuibe_lua/netboot/500_setup_server.lua
.if defined(WITH_NLS)
PLIST_FILES+=	share/locale/ru/LC_MESSAGES/dfuibe_lua.mo
.endif
.endif # WITH_LUA

##### Fetch

do-fetch:
	@if [ ! -f ${_DISTDIR}${DISTNAME}${EXTRACT_SUFX} ]; then		\
		${ECHO_MSG};							\
		${ECHO_MSG} "Distfile ${DISTNAME}${EXTRACT_SUFX} not found!";	\
		${ECHO_MSG};							\
		${ECHO_MSG} "This is an 'INTERNAL' port, meaning that the distfile is not retrieved";	\
		${ECHO_MSG} "from the Internet, but rather created from a local checkout of the";	\
		${ECHO_MSG} "BSD Installer CVS repository.  Please see the shell scripts in the";	\
		${ECHO_MSG} "scripts/build directory of the repository for more information on how";	\
		${ECHO_MSG} "to create these distfiles.";			\
		false;								\
	fi

##### Install

do-install:
	echo "Installing libaura..."
	${MKDIR} -p ${PREFIX}/include/aura
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libaura/libaura.a ${PREFIX}/lib/
	${INSTALL_PROGRAM} -o root -g wheel -m 444 ${WRKSRC}/lib/libaura/libaura.so.3 ${PREFIX}/lib/
	${LN} -sf ${PREFIX}/lib/libaura.so.3 ${PREFIX}/lib/libaura.so
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libaura/buffer.h ${PREFIX}/include/aura/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libaura/dict.h ${PREFIX}/include/aura/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libaura/popen.h ${PREFIX}/include/aura/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libaura/fspred.h ${PREFIX}/include/aura/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libaura/mem.h ${PREFIX}/include/aura/
	echo "Installing libdfui..."
	${MKDIR} -p ${PREFIX}/include/dfui
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libdfui/libdfui.a ${PREFIX}/lib/
	${INSTALL_PROGRAM} -o root -g wheel -m 444 ${WRKSRC}/lib/libdfui/libdfui.so.4 ${PREFIX}/lib/
	${LN} -sf ${PREFIX}/lib/libdfui.so.4 ${PREFIX}/lib/libdfui.so
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libdfui/dfui.h ${PREFIX}/include/dfui/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libdfui/dump.h ${PREFIX}/include/dfui/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libdfui/lang.h ${PREFIX}/include/dfui/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libdfui/system.h ${PREFIX}/include/dfui/
.if defined(WITH_C_BACKEND)
	echo "Installing libinstaller..."
	${MKDIR} -p ${PREFIX}/include/installer
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libinstaller/libinstaller.a ${PREFIX}/lib/
	${INSTALL_PROGRAM} -o root -g wheel -m 444 ${WRKSRC}/lib/libinstaller/libinstaller.so.5 ${PREFIX}/lib/
	${LN} -sf ${PREFIX}/lib/libinstaller.so.5 ${PREFIX}/lib/libinstaller.so
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libinstaller/commands.h ${PREFIX}/include/installer/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libinstaller/confed.h ${PREFIX}/include/installer/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libinstaller/diskutil.h ${PREFIX}/include/installer/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libinstaller/functions.h ${PREFIX}/include/installer/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libinstaller/package.h ${PREFIX}/include/installer/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/libinstaller/uiutil.h ${PREFIX}/include/installer/
.endif
.if defined(WITH_CURSES)
	echo "Installing dfuife_curses..."
	${MKDIR} -p ${PREFIX}/share/dfuife_curses
	${INSTALL_PROGRAM} -o root -g wheel ${WRKSRC}/frontends/ncurses/dfuife_curses ${PREFIX}/sbin/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/frontends/ncurses/fred.txt ${PREFIX}/share/dfuife_curses/
.if defined(WITH_NLS)
	for _language in ${LANGUAGES}; do \
		${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/frontends/ncurses/po/$${_language}.mo \
		    ${LOCALEDIR}/$${_language}/LC_MESSAGES/dfuife_curses.mo; \
	done
.endif
.endif
.if defined(WITH_CGI)
	echo "Installing dfuife_cgi..."
	${MKDIR} -p ${PREFIX}/www
	${INSTALL_PROGRAM} ${WRKSRC}/frontends/cgi/dfuife.cgi ${PREFIX}/www
	${INSTALL_DATA} ${WRKSRC}/frontends/cgi/dfly-pg.gif ${PREFIX}/www
	${INSTALL_DATA} ${WRKSRC}/frontends/cgi/fred-bg.gif ${PREFIX}/www
	${INSTALL_DATA} ${WRKSRC}/frontends/cgi/fred.png ${PREFIX}/www
	${INSTALL_DATA} ${WRKSRC}/frontends/cgi/dfuife.css ${PREFIX}/www
	${INSTALL_DATA} ${WRKSRC}/frontends/cgi/dfuife.js ${PREFIX}/www
	${INSTALL_DATA} ${WRKSRC}/frontends/cgi/index.html ${PREFIX}/www
.endif
# dfuife_qt
.if defined(WITH_QT)
	echo "Installing dfuife_qt..."
	${INSTALL_PROGRAM} -o root -g wheel -m 555 ${WRKSRC}/frontends/cgi/dfuife_qt ${PREFIX}/sbin
.endif
.if defined(WITH_C_BACKEND)
	echo "Installing dfuibe_installer..."
	${INSTALL_PROGRAM} -s -o root -g wheel -m 555 ${WRKSRC}/backend/installer/dfuibe_installer ${PREFIX}/sbin
	${MKDIR} -p ${PREFIX}/share/dfuibe_installer
	${INSTALL_DATA} -o root -g wheel -m 555 ${WRKSRC}/backend/installer/conf/cmdnames.conf ${PREFIX}/share/dfuibe_installer
.if defined(WITH_NLS)
	for _language in ${LANGUAGES}; do \
		${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/backend/installer/po/$${_language}.mo \
		    ${LOCALEDIR}/$${_language}/LC_MESSAGES/dfuibe_installer.mo; \
	done
.endif
.endif
.if defined(WITH_LUA_BACKEND)
	echo "Installing lua50..."
	${INSTALL_PROGRAM} -o root -g wheel -m 444 ${WRKSRC}/platform/lua/lib/liblua50.so ${PREFIX}/lib/
	${INSTALL_PROGRAM} -o root -g wheel -m 444 ${WRKSRC}/platform/lua/lib/liblualib50.so ${PREFIX}/lib/
	${INSTALL_PROGRAM} -o root -g wheel -m 555 ${WRKSRC}/platform/lua/bin/lua ${PREFIX}/bin/lua50
	${INSTALL_PROGRAM} -o root -g wheel -m 555 ${WRKSRC}/platform/lua/bin/luac ${PREFIX}/bin/lua50c
	echo "Installing lua50-compat5.1..."
	${MKDIR} -p ${PREFIX}/lib/lua/5.0
	${MKDIR} -p ${PREFIX}/lib/lua/${DISTNAME}
	${MKDIR} -p ${PREFIX}/share/lua/5.0
	${INSTALL_DATA} ${WRKSRC}/lib/lua/compat-5.1/compat-5.1.lua ${PREFIX}/share/lua/5.0
	${INSTALL_DATA} ${WRKSRC}/lib/lua/compat-5.1/compat-5.1.c ${PREFIX}/lib/lua/${DISTNAME}
	${INSTALL_DATA} ${WRKSRC}/lib/lua/compat-5.1/compat-5.1.h ${PREFIX}/lib/lua/${DISTNAME}
	${INSTALL_SCRIPT} ${WRKSRC}/lib/lua/compat-5.1/lua50c51.sh ${PREFIX}/bin/lua50c51
	echo "Installing lua50-POSIX..."
	${INSTALL_DATA} ${WRKSRC}/lib/lua/posix/lposix.so ${PREFIX}/lib/lua/5.0/
	${INSTALL_DATA} ${WRKSRC}/lib/lua/posix/posix.lua ${PREFIX}/share/lua/5.0/
	echo "Installing lua50-pty..."
	${INSTALL_DATA} ${WRKSRC}/lib/lua/pty/lpty.so ${PREFIX}/lib/lua/5.0
	${INSTALL_DATA} ${WRKSRC}/lib/lua/pty/pty.lua ${PREFIX}/share/lua/5.0
	echo "Installing lua50-filename..."
	${INSTALL_DATA} ${WRKSRC}/lib/lua/filename/filename.lua ${PREFIX}/share/lua/5.0/filename.lua
	echo "Installing lua50-app..."
	${INSTALL_DATA} ${WRKSRC}/lib/lua/app/app.lua ${PREFIX}/share/lua/5.0/app.lua
	echo "Installing lua50-dfui..."
	${INSTALL_PROGRAM} -o root -g wheel -m 444 ${WRKSRC}/lib/lua/dfui/ldfui.so ${PREFIX}/lib/lua/5.0/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/lua/dfui/dfui.lua ${PREFIX}/share/lua/5.0/
	echo "Installing lua50-luasocket..."
	${INSTALL_PROGRAM} ${WRKSRC}/lib/lua/luasocket/lsocket.so ${PREFIX}/lib/lua/5.0/
	${INSTALL_PROGRAM} ${WRKSRC}/lib/lua/luasocket/lmime.so ${PREFIX}/lib/lua/5.0/
	${INSTALL_DATA} ${WRKSRC}/lib/lua/luasocket/lua/*.lua ${PREFIX}/share/lua/5.0/
	echo "Installing lua50-transceiver..."
	${INSTALL_DATA} ${WRKSRC}/lib/lua/transceiver/transceiver.lua ${PREFIX}/share/lua/5.0/
.if defined(WITH_CURSES)
	echo "Installing lua50-lcurses..."
	${INSTALL_PROGRAM} ${WRKSRC}/lib/lua/lcurses/lcurses.so ${PREFIX}/lib/lua/5.0
	${INSTALL_DATA} ${WRKSRC}/lib/lua/lcurses/curses.lua ${PREFIX}/share/lua/5.0/
.endif
.if defined(WITH_NLS)
	echo "Installing lua50-gettext..."
	${INSTALL_PROGRAM} -o root -g wheel -m 444 ${WRKSRC}/lib/lua/gettext/lgettext.so ${PREFIX}/lib/lua/5.0/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/lib/lua/gettext/gettext.lua ${PREFIX}/share/lua/5.0/
.endif
	echo "Installing dfuibe_lua..."
	${MKDIR} -p ${DFUIBE_LUA_DIR}
	${MKDIR} -p ${DFUIBE_LUA_DIR}/lib
	${MKDIR} -p ${DFUIBE_LUA_DIR}/conf
	${MKDIR} -p ${DFUIBE_LUA_DIR}/pit
	${MKDIR} -p ${DFUIBE_LUA_DIR}/install
	${MKDIR} -p ${DFUIBE_LUA_DIR}/configure
	${MKDIR} -p ${DFUIBE_LUA_DIR}/configure/menu
	${MKDIR} -p ${DFUIBE_LUA_DIR}/upgrade
	${MKDIR} -p ${DFUIBE_LUA_DIR}/netboot
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/backend/lua/*.lua ${DFUIBE_LUA_DIR}/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/backend/lua/lib/*.lua ${DFUIBE_LUA_DIR}/lib/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/backend/lua/conf/*.lua ${DFUIBE_LUA_DIR}/conf/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/backend/lua/pit/*.lua ${DFUIBE_LUA_DIR}/pit/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/backend/lua/install/*.lua ${DFUIBE_LUA_DIR}/install/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/backend/lua/configure/*.lua ${DFUIBE_LUA_DIR}/configure/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/backend/lua/configure/menu/*.lua ${DFUIBE_LUA_DIR}/configure/menu/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/backend/lua/upgrade/*.lua ${DFUIBE_LUA_DIR}/upgrade/
	${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/backend/lua/netboot/*.lua ${DFUIBE_LUA_DIR}/netboot/
.if defined(WITH_NLS)
	for _language in ${LANGUAGES}; do \
		${INSTALL_DATA} -o root -g wheel -m 444 ${WRKSRC}/backend/lua/po/$${_language}.mo \
		    ${LOCALEDIR}/$${_language}/LC_MESSAGES/dfuibe_lua.mo; \
	done
.endif
.endif # WITH_LUA_BACKEND

OSTYPE!=sysctl -n kern.ostype

.if ${OSTYPE} == "FreeBSD"
.include <bsd.port.mk>
.endif

.if ${OSTYPE} == "DragonFly"
.include <bsd.dfport.mk>
.endif

.if ${MACHINE_ARCH:L} == "amd64"
CFLAGS+=        -fPIC
.endif

