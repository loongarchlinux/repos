# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Robin Candau <antiz@archlinux.org>
# Contributor: Eric Bélanger <eric@archlinux.org>

pkgname=gajim
pkgver=1.9.3
pkgrel=1
pkgdesc="Full featured and easy to use XMPP (Jabber) client"
url="https://gajim.org/"
arch=('any')
license=('GPL-3.0-only')
depends=('gtk3' 'gtksourceview4' 'python-cairo' 'python-gobject' 'python-keyring' 'python-nbxmpp' 'python-cryptography' 'python-precis_i18n' 'python-css-parser' 'python-distro' 'hicolor-icon-theme' 'python-pillow' 'python-gssapi' 'python-netifaces' 'python-qrcode' 'python-omemo-dr' 'python-packaging' 'pango' 'sqlite' 'python-sqlalchemy' 'python-setuptools' 'python-emoji')
makedepends=('python-build' 'python-installer' 'python-wheel')
optdepends=('python-dbus: to have gajim-remote working'
            'python-sentry_sdk: for Sentry error reporting to dev.gajim.org (users decide whether to send reports or not)'
            'gspell: for spell checking support'
            'libsecret: for GNOME Keyring or KDE support as password storage'
            'gupnp-igd: for better NAT traversing'
            'networkmanager: for network lose detection'
            'geoclue2: share current location'
            'gsound: Notification Sounds'
            'libayatana-appindicator: for App Indicator on Wayland'
            'farstream: for video and audio calls'
            'gstreamer: for video and audio calls'
            'gst-plugins-base: for video and audio calls'
            'gst-plugins-ugly: for video and audio calls'
            'gst-libav: for video and audio calls'
            'gst-plugin-gtk: for video and audio calls'
            'libxss: for idle time checking on X11'
            'python-gnupg: encrypting chat messages with OpenPGP'
            'emoji-font: for emojis support')
source=("https://dev.gajim.org/gajim/gajim/-/archive/${pkgver}/gajim-${pkgver}.tar.gz"
        disable-failing-test.patch)
sha512sums=('19a4dfed6116e62b2cd692192b472f0cc2965364d6d14c053d25816bb55a03a9d552b3ef239ba19c07ca3bc3b74fd53d32cc1d075d1a3c7e6d58cf2edf74a1c4'
            '6244bf8738baf57e391140a7df7f270394b05055ebdf57acd5f30ffd0afec542ccd4348e59a7c64a1ecfb7b7d29ef21e2f823ea765a5281eba63692b9ab488f3')
b2sums=('69366379d4c928197f6553378c28cd92e120a9006e8aa1de4c1dbd63efe688124d3e1213b801f478b8326ba5e3ef12e2562348de1340db5d3c939ee02ebd7923'
        '4bcc5859ea58bee9fabb2888172aed80bfe240bc5888c9795e382ddc511b51b7f0f5b63e6c207370e182ed41bc08242f8f38574dddf26803c30fda465924870c')

prepare() {
	cd "${pkgname}-${pkgver}"
	patch -p1 -i ../disable-failing-test.patch # Disable test that fails with pango
}

build() {
	cd "${pkgname}-${pkgver}"
	./pep517build/build_metadata.py -o dist/metadata
	python -m build --wheel --no-isolation
}

check() {
	cd "${pkgname}-${pkgver}"
	python -m unittest discover -s test
}

package() {
	cd "${pkgname}-${pkgver}"
	python -m installer --destdir="${pkgdir}" dist/*.whl
	./pep517build/install_metadata.py dist/metadata --prefix="${pkgdir}/usr"
}
