# homebrew-router
This is a collection of the configs necessary for a simple home/office router running on Ubuntu, offering DHCP and DNS service to clients on its LAN, and (optionally) an outbound VPN tunnel for moving vulnerable (DNS, HTTP, and any other non-natively-encrypted protocols) transmission endpoints outside the local ISP's reach.

The configs shown here assume an installation of the following packages has already been performed on Ubuntu 16.04 LTS:

* isc-dhcp-server
* bind9
* openvpn

For a VPN endpoint server, you'll also need:

* easy-rsa

Also recommended, for monitoring:

* ntop-ng (available from repositories as ntopng)
* netdata (available from https://github.com/firehol/netdata/wiki/Installation)
