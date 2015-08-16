# Maintainer : Mizki Suzumori <mizki9577 at gmail dot com>

pkgname=mikutter-svn
pkgver=1130
pkgrel=2
pkgdesc="a moest twitter client"
arch=('i686' 'x86_64')
url="http://mikutter.hachune.net/"
license=('GPL3')
depends=('ruby-gtk2' 'ruby-cairo')
optdepends=('libnotify: notify support')
makedepends=('subversion')
conflifts=('mikutter' 'mikutter-svn')
provides=('mikutter')

source=()
md5sums=('SKIP')

_svntrunk='svn://toshia.dip.jp/mikutter/trunk'
_svnmod="mikutter"

build() {
	cd ${srcdir}
	msg "Getting sources..."
	if [ -d ${_svnmod}/.svn ]; then
		svn update ${_svnmod}
		msg "The local files are updated..."
	else
		svn checkout ${_svntrunk} --config-dir ./ ${_svnmod}
	fi
	msg "SVN checkout done or server timeout"
}

package() {
	mkdir ${pkgdir}/opt
	cp -R ${srcdir}/${_svnmod} ${pkgdir}/opt

	rm -rf $(find ${pkgdir} -type d -name ".svn")

	mkdir -p ${pkgdir}/usr/bin
	cat <<EOF > ${pkgdir}/usr/bin/mikutter
#!/bin/sh
ruby /opt/mikutter/mikutter.rb $@
EOF
	chmod a+x ${pkgdir}/usr/bin/mikutter
}
