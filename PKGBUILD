# Maintainer: Bradford Smith <aur@bradfords.me>

pkgname=informant
pkgver=0.6.0
pkgrel=2
pkgdesc="An Arch Linux News reader and pacman hook"
arch=('any')
url="https://github.com/bradford-smith94/$pkgname"
license=('MIT')
install=informant.install
makedepends=('python-setuptools')
depends=('python' 'python-docopt' 'python-dateutil' 'python-feedparser' 'python-html2text' 'python-cachecontrol' 'python-lockfile' 'python-psutil')
source=("https://github.com/bradford-smith94/$pkgname/archive/v$pkgver.tar.gz"
        'informant.sysusers'
        'informant.tmpfiles')
options=(zipman)
sha256sums=('aa1acb6677c70f389aee64efa706ae0c87c6339ae18d501f83fefa1c8bb750b4'
            '440447f154b119fa5e3568a9ccc97fbf09326cd4c24d628d80dc02106069c6d2'
            'd05c6953c7719e3ae2958394248254eaf951da7043316a8a50a3a3c6f31b64ce')


build() {
    cd "$srcdir/$pkgname-$pkgver"
    /usr/bin/python setup.py build
}

package() {
    install -Dm 644 "${pkgname}.sysusers" "${pkgdir}/usr/lib/sysusers.d/${pkgname}.conf"
    install -Dm 644 "${pkgname}.tmpfiles" "${pkgdir}/usr/lib/tmpfiles.d/${pkgname}.conf"

    cd "$srcdir/$pkgname-$pkgver"
    export PYTHONHASHSEED=0
    /usr/bin/python setup.py install --root="${pkgdir}" --optimize=1 --skip-build
    install -Dm 0644 $pkgname.hook -T $pkgdir/usr/share/libalpm/hooks/00-$pkgname.hook
    install -Dm 0644 LICENSE -t $pkgdir/usr/share/licenses/$pkgname/
    install -Dm 0644 man/$pkgname.1 -t $pkgdir/usr/share/man/man1/
}
