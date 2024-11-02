``` shell
iptables -t nat -A POSTROUTING -p tcp -d 122.246.0.178 --dport 21754 -j MASQUERADE
iptables -t nat -A PREROUTING -p tcp --dport 8888 -j DNAT --to-destination 122.246.0.178:21754
```
