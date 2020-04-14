# vpn-whitelist

Whitelist addresses (domains and IPs) to bypass an active VPN connection. This entails
adding specific routes to the routing table and optionally (`--ufw/-u`) creating a
whitelist rule in UFW

You can do this manually using `# vpn-whitelist [address [address ...]] (--remove/-r)`
or by adding entries to `/etc/vpn-whitelist.conf` if you are using NetworkManager.

If you are curious how exactly it works, feel free to read the sources, this is mostly
for private use.
