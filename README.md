#### Create a new chain

```
iptables -t nat -N trojan
```

#### Ignore your trojan servers' addresses (replacing your-server*.com)

```
iptables -t nat -A trojan -d your-server1.com -j RETURN
iptables -t nat -A trojan -d your-server2.com -j RETURN
```

#### Ignore LANs and any other addresses you'd like to bypass the proxy

```
iptables -t nat -A trojan -d 0.0.0.0/8 -j RETURN
iptables -t nat -A trojan -d 10.0.0.0/8 -j RETURN
iptables -t nat -A trojan -d 127.0.0.0/8 -j RETURN
iptables -t nat -A trojan -d 169.254.0.0/16 -j RETURN
iptables -t nat -A trojan -d 172.16.0.0/12 -j RETURN
iptables -t nat -A trojan -d 192.168.0.0/16 -j RETURN
iptables -t nat -A trojan -d 224.0.0.0/4 -j RETURN
iptables -t nat -A trojan -d 240.0.0.0/4 -j RETURN
```

#### Anything else should be redirected to trojan's local port (udp seems not supported)

```
iptables -t nat -A trojan -p tcp -j REDIRECT --to-ports 12345
#iptables -t nat -A trojan -p udp -j REDIRECT --to-ports 12345
```

#### Apply the rules (udp seems not supported)

```
iptables -t nat -A OUTPUT -p tcp -j trojan
#iptables -t nat -A OUTPUT -p udp -j trojan
```
