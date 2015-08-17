# Maintainer: M0Rf30

pkgname='pyload-hg'
pkgver=2425
pkgrel=1
pkgdesc="Downloadtool for One-Click-Hoster written in python. Latest hg pull."
url="http://bitbucket.org/spoob/pyload/"
license='GPL'
arch=('any')
provides=('pyload')
conflicts=('pyload')
depends=('python2' 'pycrypto' 'python2-pycurl' 'tesseract' 'python-imaging' 'python2-jinja' 'python-beaker')
optdepends=('python2-qt: Gui'
            'python-flup: for additional webservers'
	    'python-notify: Notifications for GUI'
	    'js: ClickNLoad')
makedepends=('mercurial')

source=('http://bitbucket.org/ranan/pyload-dist/raw/bf705af8f412/debian/pyload/usr/share/applications/pyload-gui.desktop' 
        'http://bitbucket.org/ranan/pyload-dist/raw/bf705af8f412/debian/pyload/usr/share/applications/pyload.desktop' 
        'http://bitbucket.org/ranan/pyload-dist/raw/bf705af8f412/debian/pyload/usr/share/pixmaps/pyload-gui.png' 
        'http://bitbucket.org/ranan/pyload-dist/raw/bf705af8f412/debian/pyload/usr/share/pixmaps/pyload.svg' )

md5sums=('b96a4e5091463b3b7fd79208623f1a3a'
         'c67462993d27d5884677dd6e8a8a17d2'
         '73fcec930d25a49e1b99576069d88bd5' 
         '649d5af94101655d37fe50e7b127d1b6' )



_hgroot='http://bitbucket.org/spoob'
_hgrepo='pyload'

build() {

  cd ${srcdir}

  if [ -d $_hgrepo ]; then
    cd $_hgrepo && hg pull -u
  else
    hg clone ${_hgroot}/${_hgrepo}
    cd $_hgrepo
  fi

  hg update -C stable  


  cd ${srcdir}

  sed -i 's_#!/usr/bin/env python$_#!/usr/bin/env python2_' pyload/pyLoad*.py

  mkdir ${pkgdir}/opt
    
  cp -r ${_hgrepo} ${pkgdir}/opt/ || return 1

  install -d ${pkgdir}/usr/share/applications || return 1
  cp pyload.desktop ${pkgdir}/usr/share/applications || return 1
  cp pyload-gui.desktop ${pkgdir}/usr/share/applications || return 1

  install -d ${pkgdir}/usr/share/pixmaps || return 1
  cp pyload.svg ${pkgdir}/usr/share/pixmaps || return 1
  cp pyload-gui.png ${pkgdir}/usr/share/pixmaps || return 1

  install -d ${pkgdir}/usr/bin || return 1
  ln -s /opt/pyload/pyLoadCore.py ${pkgdir}/usr/bin/pyLoadCore || return 1
  ln -s /opt/pyload/pyLoadCli.py ${pkgdir}/usr/bin/pyLoadCli || return 1
  ln -s /opt/pyload/pyLoadGui.py ${pkgdir}/usr/bin/pyLoadGui || return 1
  

}
