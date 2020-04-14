pkgname='vpn-whitelist'
pkgver=1.0.0
pkgrel=1
arch=('any')
depends=('python')
optdepends=('networkmanager: support for automatic whitelisting of addresses'
            'ufw: support for whitelisting addresses in UFW')
backup=('etc/vpn-whitelist.conf')
source=('vpn-whitelist'
        'vpn-whitelist.conf'
        'vpn-whitelist.NetworkManager-dispatcher')
md5sums=('c8ea971cf052184ca52c58ef7c76f2eb'
         'ccdcba5f71fed613675a23a6c458d343'
         'be3c9a68a228795f0868f60ef744d061')


package() {
    # /usr/bin
    usr_bin="$pkgdir/usr/bin"
    install -D --mode 755 'vpn-whitelist' --target-directory "$usr_bin"

    # /etc
    etc="$pkgdir/etc"
    install -D --mode 644 'vpn-whitelist.conf' --target-directory "$etc"

    # /etc/NetworkManager/dispatcher.d
    install -D --mode 755 'vpn-whitelist.NetworkManager-dispatcher' --target-directory "$etc/NetworkManager/dispatcher.d"
}
