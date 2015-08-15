# Maintainer: Xu Fasheng <fasheng.xu[AT]gmail.com>
# Contributor: dongfengweixiao <dongfengweixiao[AT]gmail.com>

pkgname=deepin-media-player
pkgver=1.1+20140703161214
pkgrel=1
pkgdesc='New multimedia player with brilliant and tweakful UI. PyGtk and Deepin-ui Mplayer2 front-end, with features likes smplayer, but has a brilliant and tweakful UI.'
arch=('any')
url="http://www.linuxdeepin.com/"
license=('GPL3')
depends=('python2-scipy' 'python2-pyquery' 'deepin-ui' 'mplayer2' 'gstreamer0.10-ugly' 'gstreamer0.10-ugly-plugins' 'python2-formencode' 'gstreamer0.10-python' 'python2-chardet' 'python2-beautifulsoup3' 'python2-notify' 'python2-dbus' 'python2-xlib' )

_fileurl="http://packages.linuxdeepin.com/deepin/pool/main/d/deepin-media-player/deepin-media-player_1.1+20140703161214~6ac6ea0a8b.tar.gz"
source=("${_fileurl}")
sha256sums=('6988949977f01ab49a3ed441564aed858ee4434ee20c560d2cbd624cc7a3334b')

_filename="$(basename "${_fileurl}")"
_filename="${_filename%.tar.gz}"
_innerdir="${_filename/_/-}"

_install_copyright_and_changelog() {
    mkdir -p "${pkgdir}/usr/share/doc/${pkgname}"
    cp -f debian/copyright "${pkgdir}/usr/share/doc/${pkgname}/"
    gzip -c debian/changelog > "${pkgdir}/usr/share/doc/${pkgname}/changelog.gz"
}

# Usage: _easycp dest files...
_easycp () {
    local dest=$1; shift
    mkdir -p "${dest}"
    cp -R -t "${dest}" "$@"
}

package() {
    cd "${srcdir}/${_innerdir}"

    _easycp "${pkgdir}"/usr/share/icons/hicolor/128x128/apps/ debian/deepin-media-player.png
    _easycp "${pkgdir}"/usr/share/deepin-media-player/ locale
    _easycp "${pkgdir}"/usr/share/deepin-media-player/ app_theme
    _easycp "${pkgdir}"/usr/share/deepin-media-player/ image
    _easycp "${pkgdir}"/usr/share/deepin-media-player/ skin
    _easycp "${pkgdir}"/usr/share/deepin-media-player/ src
    _easycp "${pkgdir}"/usr/share/deepin-media-player/ tools
    _easycp "${pkgdir}"/usr/share/deepin-media-player/ AUTHORS
    _easycp "${pkgdir}"/usr/share/deepin-media-player/ README
    _easycp "${pkgdir}"/usr/share/deepin-media-player/ COPYING

    mkdir -p "${pkgdir}"/usr/share/applications
    install -m 0644 debian/deepin-media-player.desktop "${pkgdir}"/usr/share/applications/

    _install_copyright_and_changelog

    # Post install
    mkdir -p "${pkgdir}"/usr/bin
    ln -s /usr/share/deepin-media-player/src/deepin-media-player.py "${pkgdir}"/usr/bin/deepin-media-player

    cd "${pkgdir}"/usr/share/deepin-media-player/tools
    python2 generate_mo.py

    # fix python version
    find "${pkgdir}" -iname "*.py" | xargs sed -i 's=\(^#! */usr/bin.*\)python=\1python2='
}
