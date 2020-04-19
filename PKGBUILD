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
md5sums=('f615957b38db41c6bd0f3c8577040ffe'
         '34e52d508ad14a74d5110abb3b5bad8a'
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
