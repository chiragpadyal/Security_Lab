On Both PC:
```
sudo apt-get install ipsec-tools strongswan-starter
```

On Both PC:
ipsec.conf
```
sudo gedit /etc/ipsec.conf

#on RED system 1
conn red-to-blue
	authby=secret
	auto=route
	keyexchange=ikev2
	ike=aes128-md5-modp1024
	left=192.168.1.207
	right=192.168.1.204
	type=transport
	esp=aes128-sha-modp1024!

sudo gedit /etc/ipsec.secrets
# contains
192.168.1.204 192.168.1.207 : PSK "test123"


```

On Both PC:
```
sudo ipsec start
sudo ipsec update
```

On Main Pc:
```
sudo ipsec up red-to-blue
```

Listen on Second PC:
```
sudo tcpdump -i eth0 -w ike.pcap
# restart ipsec on Red pc
wireshark ike.pcap
```
Change Password on any one pc and restart ipsec
```
# update and start ipsec on both end
sudo ipsec update
#only on main pc
sudo ipsec up red-to-blue

```
