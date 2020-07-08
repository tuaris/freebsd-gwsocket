# Created by: Daniel Morante <daniel@morante.net>
# $FreeBSD: $

PORTNAME=	gwsocket
PORTVERSION=	0.3
CATEGORIES=	www
MASTER_SITES=	http://tar.gwsocket.io/

MAINTAINER=	daniel@morante.net
COMMENT=	RFC6455 compliant WebSocket Server

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/COPYING

GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip
USES=		alias compiler:c11 pkgconfig
USE_LDCONFIG=	yes

CFLAGS+=	-I${NCURSESINC} -I${LOCALBASE}/include
LDFLAGS+=	-L${NCURSESLIB} -L${LOCALBASE}/lib

PORTDOCS=	AUTHORS COPYING ChangeLog NEWS README

OPTIONS_DEFINE=	DOCS DEBUG UTF8 OPENSSL EXAMPLES
OPTIONS_DEFAULT=	UTF8
OPTIONS_SUB=	yes

DEBUG_CONFIGURE_ON=	--enable-debug
UTF8_CONFIGURE_ON=	--enable-utf8

OPENSSL_USES=           ssl
OPENSSL_CONFIGURE_ON=   --with-openssl=${OPENSSLBASE}

USE_RC_SUBR=	${PORTNAME}
SUB_LIST+=	PORTNAME=${PORTNAME} \
			DEFAULT_USER=www \
			DEFAULT_GROUP=www

SUB_FILES=      pkg-message

do-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S,^,${WRKSRC}/,} ${STAGEDIR}${DOCSDIR}

post-install-EXAMPLES-on:
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${FILESDIR}/sample.html ${STAGEDIR}${EXAMPLESDIR}

post-install:
	${INSTALL_DATA} ${FILESDIR}/${PORTNAME}.conf \
		${STAGEDIR}${PREFIX}/etc/${PORTNAME}.conf.sample

.include <bsd.port.mk>
