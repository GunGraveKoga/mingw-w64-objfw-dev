
_compiler=clang

_realname=objfw-dev
pkgbase=mingw-w64-${_realname}

pkgname=("${MINGW_PACKAGE_PREFIX}-${_realname}")

pkgver=0.9.dev
pkgrel=2
pkgdesc="A portable framework for the Objective-C language (mingw-w64)"
arch=('any')
url="https://heap.zone/objfw/"
license=("GPL")
makedepends=("autoconf"
			 "unzip"
			 "make"
			 "${MINGW_PACKAGE_PREFIX}-binutils"
			 "${MINGW_PACKAGE_PREFIX}-gcc"
			 "${MINGW_PACKAGE_PREFIX}-clang"
			 "unzip")

depends=("${MINGW_PACKAGE_PREFIX}-clang")

conflicts=("${MINGW_PACKAGE_PREFIX}-objfw-rel"
		   "${MINGW_PACKAGE_PREFIX}-objfw")

source=("https://github.com/Midar/objfw/archive/master.zip")

sha256sums=('SKIP')

noextract=(master.zip)

prepare() {
	plain "Extracting objfw-master.zip"
	[[ -d ${srcdir}/objfw-master ]] || unzip master.zip -d ${srcdir} || true

	cd "${srcdir}"/objfw-master

	[[ -f ./configure ]] || autoreconf -fi || true

}

configure_objfw() {
	cd "${srcdir}"/objfw-master

	./configure --prefix="" \
	 --enable-static \
	 --enable-runtime \
	 --enable-seluid24 \
	OBJC=${_compiler} \
	OBJCFLAGS="-O0 -g3"
}

build() {
	cd "${srcdir}"/objfw-master

	[[ -f ./buildsys.mk ]] && make distclean && configure_objfw || configure_objfw || true

	make
}

package_objfw-dev() {
	pkgdesc="A portable framework for the Objective-C language (mingw-w64)"
	url="https://heap.zone/objfw/"
	depends=("${MINGW_PACKAGE_PREFIX}-clang")

	cd "${srcdir}"/objfw-master

	make DESTDIR="${pkgdir}" install
}

package_mingw-w64-i686-objfw-dev() {
	package_objfw-dev
}

package_mingw-w64-x86_64-objfw-dev() {
	package_objfw-dev
}