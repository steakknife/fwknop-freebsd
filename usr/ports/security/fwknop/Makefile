# Created by: Sean Greven <sean.greven@gmail.com>
# $FreeBSD: head/security/fwknop/Makefile 347597 2014-03-09 14:26:25Z miwi $

PORTNAME=	fwknop
PORTVERSION=	2.6.2
PORTREVISION=	1
CATEGORIES=	security
MASTER_SITES= http://www.cipherdyne.org/fwknop/download/

MAINTAINER=	sean.greven@gmail.com
COMMENT=	SPA implementation for Linux and FreeBSD

LICENSE=	GPLv2

OPTIONS_SINGLE=	FIREWALL_TYPE
OPTIONS_SINGLE_FIREWALL_TYPE=	PF IPF IPFW
OPTIONS_DEFINE=		GPGME
OPTIONS_DEFAULT=	GPGME PF

GPGME_DESC=	Build support for gpgme
PF_DESC=	pf firewall
IPF_DESC= ipf (ipfilter) firewall
IPFW_DESC=	ipfw firewall

INFO=		libfko
GNU_CONFIGURE=	yes
USE_RC_SUBR=	fwknopd
USE_LDCONFIG=	yes

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MGPGME}
LIB_DEPENDS+=	libgpgme.so:${PORTSDIR}/security/gpgme
.else
CONFIGURE_ARGS+=--without-gpgme
.endif

.if	${PORT_OPTIONS:MPF}
CONFIGURE_ARGS+= --with-pf=/sbin/pfctl
.endif

.if	${PORT_OPTIONS:MIPF}
CONFIGURE_ARGS+= --with-ipf=/sbin/ipf
.endif

.if	${PORT_OPTIONS:MIPFW}
CONFIGURE_ARGS+= --with-ipfw=/sbin/ipfw
.endif

post-build:
	cd $(WRKSRC)/test && ./test-fwknop.pl --enable-all

.include <bsd.port.mk>
