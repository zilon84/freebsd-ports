# $FreeBSD$

PORTNAME=	klayout
PORTVERSION=	0.23.8
CATEGORIES=	cad
MASTER_SITES=	http://178.77.72.242/downloads/

MAINTAINER=	hrs@FreeBSD.org
COMMENT=	Qt-based GDS2 Viewer

LICENSE=	GPLv2

USES=		gmake
USE_RUBY=	yes
USE_QT4=	corelib designer gui network moc_build sql uic_build \
		rcc_build qt3support xml
PLIST_FILES=	bin/klayout \
		bin/strm2cif \
		bin/strm2dxf \
		bin/strm2gds \
		bin/strm2oas \
		bin/strm2txt \
		bin/strmclip \
		bin/strmcmp \
		bin/strmxor \
		lib/libklayout.so
PLATFORMKEYWORD=freebsd-32-gcc-release

BROKEN_sparc64=	Does not compile on sparc64: gcc bug

do-build:
	cd ${WRKSRC} && \
	    ${SETENV} CC=${CC} CXX=${CXX} \
		${SH} build.sh -platform ${PLATFORMKEYWORD} \
		-qtbin ${QT_PREFIX}/bin \
		-qtinc ${QT_INCDIR} \
		-qtlib ${QT_LIBDIR}

do-install:
	cd ${WRKSRC}/bin.${PLATFORMKEYWORD} && \
	    ${INSTALL_PROGRAM} ${PLIST_FILES:Mbin/*:S,^bin/,,} \
	    ${STAGEDIR}${PREFIX}/bin
	cd ${WRKSRC}/build.${PLATFORMKEYWORD}/main && \
	    ${INSTALL_LIB} ${PLIST_FILES:Mlib/*:S,^lib/,,} \
	    ${STAGEDIR}${PREFIX}/lib

.include <bsd.port.mk>
