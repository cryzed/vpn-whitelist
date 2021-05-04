# vpn-whitelist

Small foreword: I realize how complex many network configurations are and how vastly
they can differ: some people might dislike `UFW` and prefer using `iptables` directly,
or don't use `NetworkManager` at all. Please keep in mind that this is _mostly_ for my
private use. I released this just in case someone else has a use for it, and I spend too
much time on it not to share it -- this is all to say, I most likely won't add options
for your specific network configuration and wishes if this doesn't do it for you.

Whitelist addresses (domains and IPs) to bypass an active VPN connection. This entails
adding specific routes to the routing table and optionally creating a whitelist rule in
UFW. These rules and routes can be easily removed later.

If you use and have enabled `NetworkManager` and `NetworkManager-dispatcher`
systemd-units, you can also put addresses in `/etc/vpn-whitelist.conf` to be
automatically whitelisted when a VPN tunnel goes up and remove them when it goes down.
Alternatively you can run and enable the provided `systemd` service:

`$ sudo systemctl enable --now vpn-whitelist`

Or run the daemon yourself:

`# vpn-whitelist --daemon`


```
$ vpn-whitelist --help
usage: vpn-whitelist [-h] [--remove] [--file FILES] [--interface INTERFACE] [--gateway GATEWAY] [--ufw] [--table TABLE] [--dry-run] [--comment COMMENT] [--daemon] [--interval INTERVAL] [address ...]

positional arguments:
  address               Domains or IPs to be whitelisted (default: None)

optional arguments:
  -h, --help            show this help message and exit
  --remove, -r          Remove the ip routes (and optionally UFW rules) instead (default: False)
  --file FILES, -f FILES
                        Load addresses from a file, repeatable (default: [])
  --interface INTERFACE, -i INTERFACE
                        Manually specify the network interface through which to route the traffic (default: None)
  --gateway GATEWAY, -g GATEWAY
                        Manually specify the network interface's gateway (default: None)
  --ufw, -u             Create UFW whitelist rules (default: False)
  --table TABLE, -t TABLE
                        The target routing table (default: main)
  --dry-run, -d         Do nothing, only print the changes to the network configuration (default: False)
  --comment COMMENT, -c COMMENT
                        Comment used for the UFW whitelist rule (default: None)
  --daemon, -D          Run daemon (default: False)
  --interval INTERVAL, -I INTERVAL
                        The interval the daemon waits before checking for changed network interfaces (default: 1)
```


This is a DNS proxy that monitors requested domains, automatically whitelists them
using `vpn-whitelist` if any of the provided regular expressions match and then forwards
the reply. This is obviously not possible with just `vpn-whitelist` because there's no
easy way to find all domains and sub-domains that match a given regular expression -- so
we simply monitor which domains your system is trying to resolve, and match on those.

A use-case scenario would for example be regional game servers: `[XX].game.com` where XX
is the country code, or for example video CDNs (think Twitch/YouTube) where the specific
domain chosen (and its associated A-records) is unpredictable and your VPN isn't
necessarily needed and just slows down your connection.

```
usage: vpn-whitelist-dns-proxy [-h] [-H HOST] [-p PORT] [-P REMOTE_PORT] [-k] remote_host [regexes [regexes ...]]

Unrecognized arguments will be forwarded to "vpn-whitelist"

positional arguments:
  remote_host           Remote DNS host
  regexes               Regular expressions used to match queried addresses (default: [])

optional arguments:
  -h, --help            show this help message and exit
  -H HOST, --host HOST  Address to bind to (default: localhost)
  -p PORT, --port PORT  Port to listen on (default: 53)
  -P REMOTE_PORT, --remote-port REMOTE_PORT
                        Remote DNS port (default: 53)
  -k, --keep            Don't remove whitelisted addresses during exit (default: False)
```


If you are curious how exactly it works, feel free to read the sources, this is mostly
for private use. Please note that this currently only supports IPv4, mostly because I
have IPv6 disabled on my system (my VPN doesn't support it) and would have trouble
supporting it. Adding support for AAAA-records (IPv6) to `vpn-whitelist-dns-proxy` would
be trivial however.
