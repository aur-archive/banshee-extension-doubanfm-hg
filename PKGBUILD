# Maintainer: L42y <423300@gmail.com>
pkgname=banshee-extension-doubanfm-hg
pkgver=34
pkgrel=5
pkgdesc="Douban FM extension for Banshee"
arch=('i686' 'x86_64')
url="https://bitbucket.org/pro711/banshee-doubanfm/wiki/Home"
license=('MIT')
depends=('banshee')
makedepends=('mercurial' 'gnome-doc-utils' 'intltool' 'autoconf')
provides=('banshee-extension-doubanfm')
conflicts=('banshee-extension-doubanfm')
install=

hgroot="https://bitbucket.org/pro711/banshee-doubanfm"
hgrepo="banshee-doubanfm"

build() {
  cd "$srcdir"
  msg "Connecting to Mercurial server...."

  if [ -d $hgrepo ] ; then
    cd $hgrepo
    hg pull -u
    msg "The local files are updated."
  else
    hg clone $hgroot $hgrepo
  fi

  msg "Mercurial checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$hgrepo-build"
  cp -r "$srcdir/$hgrepo" "$srcdir/$hgrepo-build"
  cd "$srcdir/$hgrepo-build"

  #
  # BUILD HERE
  #
  
  ### Temporary fix for upstream Issue #14
  ### See https://bitbucket.org/pro711/banshee-doubanfm/issue/14/archlinux for more details.
  sed -i 's/AM_CONFIG_HEADERS/AC_CONFIG_HEADERS/g' ./configure.ac

  ./autogen.sh --prefix=/usr
  make
}

package() {
  cd "$srcdir/$hgrepo-build"
  make DESTDIR="$pkgdir/" install
} 
