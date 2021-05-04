pkgname='vpn-whitelist'
pkgver=1.1.0
pkgrel=1
arch=('any')
depends=('python')
optdepends=('networkmanager: support for automatic whitelisting of addresses'
            'ufw: support for whitelisting addresses in UFW')
backup=('etc/vpn-whitelist.conf')
source=('vpn-whitelist'
        'vpn-whitelist-dns-proxy'
        'vpn-whitelist.conf'
        'vpn-whitelist.NetworkManager-dispatcher'
        'vpn-whitelist.service')
md5sums=('844d183c08133db6b29eccc150fec483'
         'f9c4585de99299014e72d366e8a8e676'
         '975da211e2ff74b472a938dca6f646b9'
         '00037bd5bc12a3e4a35251b8b83c86ee'
         '8ff50a3216e3d3de8b231b1fab163ef8')


package() {
    # /usr/bin
    usr_bin="$pkgdir/usr/bin"
    install -D --mode 755 'vpn-whitelist' --target-directory "$usr_bin"
    install -D --mode 755 'vpn-whitelist-dns-proxy' --target-directory "$usr_bin"

    # /etc
    etc="$pkgdir/etc"
    install -D --mode 644 'vpn-whitelist.conf' --target-directory "$etc"

    # /etc/NetworkManager/dispatcher.d
    #install -D --mode 755 'vpn-whitelist.NetworkManager-dispatcher' --target-directory "$etc/NetworkManager/dispatcher.d"

    # /etc/systemd/system/vpn-whitelist.service
    install -D --mode 755 'vpn-whitelist.service' --target-directory "$etc/systemd/system"
}
