# Maintainer:maz-1 <loveayawaka at gmail dot com>

pkgname=chinadns-git
_gitname=ChinaDNS
pkgver=1.3.0.r21.g3d2bc8c
pkgrel=1
pkgdesc="A tool for fixing weird things with DNS in China."
arch=('i686' 'x86_64')
url="https://github.com/clowwindy/ChinaDNS"
license=('MIT')
depends=('glibc')
makedepends=('git')
provides=('chinadns' 'chinadns-c')
conflicts=('chinadns' 'chinadns-c')
source=('git+https://github.com/clowwindy/ChinaDNS.git'
		'config.cfg'
        'chinadns.service')
md5sums=('SKIP'
		 '1a2806b5861e239107246c47fa00ecca'
         '5269abd347c5ad3de55bbfc376c6657c')
pkgver() {
  cd "$srcdir"/$_gitname
  git describe --long --tags | sed -r 's/([^-]*-g)/r\1/;s/-/./g'
}

build() {
  cd "$srcdir"/$_gitname
  ./autogen.sh
  ./configure --prefix=/usr
  make
}

package() {
  cd "$srcdir"/$_gitname
  make DESTDIR="$pkgdir" install
	
  install -Dm 644 ${srcdir}/$_gitname/COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
  install -Dm 644 ${srcdir}/$_gitname/README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
  install -Dm 644 ${srcdir}/$_gitname/CHANGES "$pkgdir/usr/share/doc/$pkgname/CHANGES"
  install -Dm 644 ${srcdir}/$_gitname/chnroute.txt "$pkgdir/etc/chinadns/chnroute.txt"
  install -Dm 644 ${srcdir}/$_gitname/iplist.txt "$pkgdir/etc/chinadns/iplist.txt"
  rm "$pkgdir/usr/share/chnroute.txt" "$pkgdir/usr/share/iplist.txt"
  install -Dm 644 "$srcdir"/config.cfg "$pkgdir"/etc/chinadns/config.cfg
  install -Dm 644 ${srcdir}/chinadns.service ${pkgdir}/usr/lib/systemd/system/chinadns.service
}
 
