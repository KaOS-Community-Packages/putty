pkgname=putty-svn
pkgver=10297      
pkgrel=2
pkgdesc="A client program for the SSH, Telnet and Rlogin network protocols"
arch=('x86_64')
url="http://www.chiark.greenend.org.uk/~sgtatham/putty"
license=('MIT')
depends=('gtk2')
makedepends=('subversion' 'zip')
source=("svn://svn.tartarus.org/sgt/${pkgname%-*}"
        "https://github.com/Gabrielgtx/putty-icons/releases/download/1.0/putty.png"
        "https://github.com/Gabrielgtx/putty-icons/releases/download/1.0/putty.xpm"
        "putty.desktop")
md5sums=('SKIP'
         '568bbb54c70d12c7bb9f8d6379068b38'
         'f07f6536daedef3bd949fddcb4da1050'
         'd0d073175dc1f3ee73c1e93a4cfe1ad8')

build() {
	cd "${pkgname%-*}"
	./mkfiles.pl	
	cd unix
	make -f Makefile.gtk || return 1
}

package() {
	cd "${pkgname%-*}/unix"
	mkdir -p $pkgdir/usr/bin
  	install -Dm755 putty puttygen puttytel pterm psftp pscp plink $pkgdir/usr/bin || return 1
	install -Dm644 ../LICENCE $pkgdir/usr/share/licenses/$pkgname/LICENSE
	msg "Installing Icon and .desktop file"
	install -Dm644 "${srcdir}/putty.desktop" "${pkgdir}/usr/share/applications/putty.desktop"
        install -Dm644 "${srcdir}/putty.png" "${pkgdir}/usr/share/pixmaps/putty.png"
        install -m644 "${srcdir}/putty.xpm" "${pkgdir}/usr/share/pixmaps/putty.xpm"
}

pkgver() {
	cd "$startdir/${pkgname%-*}"
	svnversion | tr -d [A-z]
}
  
