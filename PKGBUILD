pkgname='vpn-whitelist'
pkgver=1.0.0
pkgrel=1
arch=('any')
depends=('python')
optdepends=('networkmanager: support for automatic whitelisting of addresses'
            'ufw: support for whitelisting addresses in UFW')
backup=('etc/vpn-whitelist.conf')
source=('vpn-whitelist'
        'vpn-whitelist-dns-proxy'
        'vpn-whitelist.conf'
        'vpn-whitelist.NetworkManager-dispatcher')
md5sums=('ce178bc684c5a12dfecdc0095c0ef21e'
         '7fba999a24fc7827ed961bbcf95e23d9'
         'fe878b7f244636858b8ead0714d403ee'
         '50f3b1dcbb8220b809b0877e6e7668b1')


package() {
    # /usr/bin
    usr_bin="$pkgdir/usr/bin"
    install -D --mode 755 'vpn-whitelist' --target-directory "$usr_bin"
    install -D --mode 755 'vpn-whitelist-dns-proxy' --target-directory "$usr_bin"

    # /etc
    etc="$pkgdir/etc"
    install -D --mode 644 'vpn-whitelist.conf' --target-directory "$etc"

    # /etc/NetworkManager/dispatcher.d
    install -D --mode 755 'vpn-whitelist.NetworkManager-dispatcher' --target-directory "$etc/NetworkManager/dispatcher.d"
}
