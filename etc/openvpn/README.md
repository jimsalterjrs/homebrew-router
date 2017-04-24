# creating certificates on the server

cd /etc/openvpn/
cp -a /usr/share/easy-rsa/* /etc/openvpn/

nano /etc/openvpn/vars

Replace the stuff in vars with appropriate values for your organization. Pay special attention to KEY_SIZE, KEY_EXPIRE, and CA_EXPIRE. The rest are just human-readable fluff.

source ./vars
./clean-all

You MUST run ./clean-all the first time you set up the server. However, if you run it again AFTER that, it'll clean out your entire keys directory. Be warned!

./build-ca
./build-key-server SERVERNAME
./build-dh 4096

Obviously, replace SERVERNAME with whatever server name you'd like here. Just plain "server" is a common choice.  Note that 4096 is an ambitious Diffie-Hellman key size: it's good for your paranoia, but it WILL take a SIGNIFICANT time to build - just under 30 minutes on a Digital Ocean $5 instance, as tested 2017-04-22!

./build-key client-no-pass
./build-key-pass client-with-pass

These will create certificate/key pairs for "client-no-pass" and "client-with-pass" in /etc/openvpn/keys.  "Client-with-pass" will, of course, have a PEM challenge phrase associated with it for extra security.

Note: if you build a lot of client keys, you may want to consider editing build-key and build-key-pass, and removing the "--interact" argument from each. This saves you from incessantly pressing Enter 10 times per key to accept the default values you set in ./vars.

systemctl enable openvpn ; systemctl start openvpn to fire it up once your keys are generated.
you'll need ca.crt, CLIENTNAME.crt, and CLIENTNAME.key from /etc/openvpn/keys on a client machine that connects into here, along with a .ovpn or .conf file defining the tunnel (sample provided here as outboundvpn.conf; just rename it to outboundvpn.ovpn if you're on Windows.)

