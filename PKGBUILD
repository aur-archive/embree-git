pkgname=embree-git
_pkgname=embree
pkgver=r2385.98b2d5e
pkgrel=1
pkgdesc='Embree High Performance Ray Tracing Kernels'
arch=('any')
url="https://embree.github.io/"
license=('Apache 2.0')
depends=('freeglut' 'libxmu' 'libxi')
makedepends=('git' 'cmake' 'ispc')
provides=('embree')
conflicts=('embree')

source=('embree::git+https://github.com/embree/embree.git')

md5sums=('SKIP')

pkgver() {
  cd "$_pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	cd $srcdir/$_pkgname
	mkdir build
	cd build
	cmake ..
	cmake . -DCMAKE_INSTALL_PREFIX:PATH=/usr
	cmake . -DBUILD_TUTORIALS=OFF
	cmake . -DBUILD_TUTORIALS_ISPC=OFF
	cmake . -DXEON_PHI_ISA=OFF	
	make
	wget http://www.apache.org/licenses/LICENSE-2.0
}


package() {
	cd $srcdir/$_pkgname/build
	make install DESTDIR=$pkgdir
	install -D -m644 LICENSE-2.0 $pkgdir/usr/share/licenses/$_pkgname/LICENSE
}
