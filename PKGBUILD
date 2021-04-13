pkgname=putty
pkgver=0.74
pkgrel=1
pkgdesc="A client program for the SSH, Telnet and Rlogin network protocols"
arch=('x86_64')
url="http://www.chiark.greenend.org.uk/~sgtatham/putty"
license=('MIT')
depends=('gtk3')
source=("http://the.earth.li/~sgtatham/putty/latest/${pkgname}-${pkgver}.tar.gz"
        "putty.png"
        "putty.desktop")
md5sums=('dbfa58f22a91b22b7489173e9dd09e30'
         '568bbb54c70d12c7bb9f8d6379068b38'
         'd0d073175dc1f3ee73c1e93a4cfe1ad8')

build() {
	cd ${pkgname}-${pkgver}/unix
	sed -i -e 's/-Werror//g' ../configure Makefile.ux Makefile.gtk
	./configure --prefix=/usr
	make
}

package() {
	cd "${pkgname}-${pkgver}/unix"
	make DESTDIR="${pkgdir}" install
	install -Dm644 ../LICENCE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	msg "Installing Icon and .desktop file"
	install -Dm644 "${srcdir}/putty.desktop" "${pkgdir}/usr/share/applications/putty.desktop"
	install -Dm644 "${srcdir}/putty.png" "${pkgdir}/usr/share/pixmaps/putty.png"
}
