# Maintainer: Pierre Neidhardt <ambrevar at gmail dot com>

pkgname=musish-git
_pkgname=musish
pkgver=4e6df4c
pkgrel=1
pkgdesc="A dynamic and extensible music library organizer"
url="http://bitbucket.org/ambrevar/$_pkgname/"
arch=('any')
license=('MIT')
depends=('ffmpeg' 'dash')
optdepends=('jshon' 'cuetools')
source=(git+https://bitbucket.org/ambrevar/"${_pkgname}".git)
install="$_pkgname.install"
sha1sums=('SKIP')

pkgver() {
    cd $_pkgname
    git describe --always | sed 's|-|.|g'
}

## This patch runs dash instead of bash (slightly faster). You can safely
## comment this and remove 'dash' from the depends if you do not want it.
prepare () {
    cd "${srcdir}/${_pkgname}"
    ex -sc '%s/#!\/bin\/sh/#!\/bin\/dash/|xit' musish
}

package() {
    cd "${srcdir}/${_pkgname}"
    install -D -m755 musish "${pkgdir}/usr/bin/musish"
    install -D -m755 titlecase "${pkgdir}/usr/bin/titlecase"
    install -D -m644 musishrc "${pkgdir}/etc/xdg/musish/musishrc"
    install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${_pkgname}/LICENSE"

    for i in scripts/*; do
        install -D -m755 "$i" "${pkgdir}/usr/share/${_pkgname}/$i"
    done

    ## Man page
    install -D -m755 -d "${pkgdir}/usr/share/man/man1/"
    gzip -c musish.1 > "${pkgdir}/usr/share/man/man1/musish.1.gz" && chmod 644 "${pkgdir}/usr/share/man/man1/musish.1.gz"
}
