### motivation
```
wsl2:~ $ ping -c1 google.com
ping: socket: Operation not permitted
```

non-root users are not allowed to execute `ping`

### solution:

**temporary**
```
wsl2:~ $ sudo sysctl net.ipv4.ping_group_range="0 2147483647"
net.ipv4.ping_group_range = 0 2147483647

wsl2:~ $ ping -c1 google.com
PING google.com (142.251.36.110) 56(84) bytes of data.
64 bytes from prg03s11-in-f14.1e100.net (142.251.36.110): icmp_seq=1 ttl=117 time=17.1 ms

--- google.com ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 17.074/17.074/17.074/0.000 ms
```

**permanent**
```
wsl2:~ $ sudo sh -c 'echo net.ipv4.ping_group_range = 0 2147483647 >> /etc/sysctl.conf'
wsl2:~ $ sudo sysctl --system
* Applying /etc/sysctl.d/99-sysctl.conf ...
net.ipv4.ping_group_range = 0 2147483647
* Applying /etc/sysctl.conf ...
net.ipv4.ping_group_range = 0 2147483647

wsl2:~ $ sudo sysctl -p
net.ipv4.ping_group_range = 0 2147483647

wsl2:~ $ ping -c1 google.com
PING google.com (142.251.36.110) 56(84) bytes of data.
64 bytes from prg03s11-in-f14.1e100.net (142.251.36.110): icmp_seq=1 ttl=117 time=13.3 ms

--- google.com ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 13.303/13.303/13.303/0.000 ms
```
