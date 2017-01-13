
_compiler=clang

_realname=objfw
pkgbase=mingw-w64-${_realname}

pkgname=("${MINGW_PACKAGE_PREFIX}-${_realname}")

pkgver=dev
pkgrel=0
pkgdesc="A portable framework for the Objective-C language (mingw-w64)"
arch=('any')
url="https://heap.zone/objfw/"
license=("GPL")
makedepends=("autoconf"
			 "unzip"
			 "make"
			 "${MINGW_PACKAGE_PREFIX}-binutils"
			 "${MINGW_PACKAGE_PREFIX}-gcc"
			 "${MINGW_PACKAGE_PREFIX}-clang")

depends=("${MINGW_PACKAGE_PREFIX}-clang")

conflicts=("${MINGW_PACKAGE_PREFIX}-objfw-rel")

source=("https://github.com/Midar/objfw/archive/master.zip")

sha256sums=('SKIP')

noextract=(master.zip)

prepare() {
	plain "Extracting objfw-master.zip"
	[[ -d ${srcdir}/objfw-master ]] || unzip master.zip -d ${srcdir} || true

	cd "${srcdir}"/objfw-master

	[[ -f ./configure ]] || autoreconf || true

}

configure_objfw() {
	cd "${srcdir}"/objfw-master

	./configure --prefix="" \
	 --enable-static \
	 --enable-runtime \
	 --enable-seluid24 \
	 OBJC=clang
}

build() {
	cd "${srcdir}"/objfw-master

	[[ -f ./buildsys.mk ]] && make distclean && configure_objfw || configure_objfw || true

	make
}

package_objfw() {
	pkgdesc="A portable framework for the Objective-C language (mingw-w64)"
	url="https://heap.zone/objfw/"
	depends=("${MINGW_PACKAGE_PREFIX}-clang")

	cd "${srcdir}"/objfw-master

	make DESTDIR="${pkgdir}" install
}

package_mingw-w64-i686-objfw() {
	package_objfw
}

package_mingw-w64-x86_64-objfw() {
	package_objfw
}