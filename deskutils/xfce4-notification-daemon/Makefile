# Created by: Emanuel Haupt <ehaupt@FreeBSD.org>
# $FreeBSD$

PORTNAME=	notification-daemon
PORTVERSION=	0.3.7
PORTREVISION=	23
CATEGORIES=	deskutils xfce
MASTER_SITES=	LOCAL/ehaupt/
PKGNAMEPREFIX=	xfce4-
DISTNAME=	${PORTNAME}-xfce-${PORTVERSION}
DIST_SUBDIR=	xfce4

MAINTAINER=	ehaupt@FreeBSD.org
COMMENT=	Port of Gnome's notification-daemon for the Xfce desktop

LICENSE=	GPLv2

BUILD_DEPENDS=	p5-XML-Parser>=0:textproc/p5-XML-Parser
LIB_DEPENDS=	libsexy.so:x11-toolkits/libsexy \
		libdbus-glib-1.so:devel/dbus-glib \
		libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2
RUN_DEPENDS=	dbus-daemon:devel/dbus

DEPRECATED=	No longer supported by upstream, replaced with deskutils/xfce4-notifyd
EXPIRATION_DATE=2016-11-23

GNU_CONFIGURE=	yes
INSTALLS_ICONS=	yes
USES=		gmake libtool pkgconfig gettext-tools xfce tar:bzip2
USE_GNOME=	librsvg2 gtk20 cairo
USE_LDCONFIG=	yes
USE_XFCE=	libgui
USE_XORG=	x11

INSTALL_TARGET=	install-strip

CONFIGURE_ARGS+=	--libdir=${PREFIX}/lib/xfce4 \
			--libexecdir=${PREFIX}/libexec/xfce4 \
			--with-dbus-services=${PREFIX}/share/dbus-1/services

CONFLICTS=	notify-osd-[0-9]*

OPTIONS_DEFINE=	GRADIENT CLOSE NLS

GRADIENT_DESC=	Show a gradient look in the default theme
CLOSE_DESC=	Show the close button in the default theme

OPTIONS_DEFAULT=CLOSE

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MNLS}
USES+=		gettext-runtime
PLIST_SUB+=	NLS=""
.else
PLIST_SUB+=	NLS="@comment "
.endif

.if ${PORT_OPTIONS:MGRADIENT}
CONFIGURE_ARGS+=	--enable-gradient-look
.endif

.if ${PORT_OPTIONS:MCLOSE}
CONFIGURE_ARGS+=	--disable-close-button
.endif

post-patch:
	@${REINPLACE_CMD} -e 's|\(notification-daemon-xfce\)-1.0|\1|' \
		${WRKSRC}/src/daemon/Makefile.in \
		${WRKSRC}/src/themes/bubble/Makefile.in \
		${WRKSRC}/src/themes/standard/Makefile.in
	@${REINPLACE_CMD} '/GTK_LIBS =/s/$$/ -lgmodule-2.0 -lX11/' \
		${WRKSRC}/src/daemon/Makefile.in
.if empty(PORT_OPTIONS:MNLS)
	@${REINPLACE_CMD} -e 's|\(USE_NLS=\)yes|\1no|' ${WRKSRC}/configure
.endif

.include <bsd.port.mk>
