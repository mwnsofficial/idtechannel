---
layout: post
title:  "Redir Host dan Fake IP"
author: Muhammad Yusuf
categories: [ clash ]
image: assets/images/4.jpg
youtubeid: 
---
Saya akan membahas soal **Redir Host** dan **Fake IP**.

Pembelajaran di halaman ini menjelaskan bagaimana cara setting dan cara optimasi dari kedua hal tersebut.

**Redir Host** adalah pengalihan koneksi trafik dari dari host ke server.

Sedangkan **Fake IP** adalah pengalihan koneksi trafik dari pihak ketiga sebelum menu server.

Setting **Redir Host** dengan mengaktifkan Tun pada configuration.yaml dalam folder config.

```
dns:
  enable: true
  listen: 0.0.0.0:1053
  enhanced-mode: redir-host
  nameserver:
    - 114.114.114.114

tun:
  enable: true
  device-url: dev://clash0 #specific a TUN device
  dns-listen: 0.0.0.0:1053 #TUN dns listen port, only DNS requires bypassed it, tun can hijack them
```

Jika anda pengguna **Linux** anda bisa memulai nya dengan

```
sudo ./clash
```

Dan berikut setting routing untuk linux dan openwrt

```
# Based on https://github.com/Kr328/kr328-clash-setup-scripts/blob/master/setup-clash-tun.sh
# Make sure your clash DNS listen at 1053, otherwise you should modify some part

ipset create localnetwork hash:net
ipset add localnetwork 127.0.0.0/8
ipset add localnetwork 10.0.0.0/8
ipset add localnetwork 169.254.0.0/16
ipset add localnetwork 192.168.0.0/16
ipset add localnetwork 224.0.0.0/4
ipset add localnetwork 240.0.0.0/4
ipset add localnetwork 172.16.0.0/12
ip tuntap add user root mode tun clash0
ip link set clash0 up
ip address replace 172.31.255.253/30 dev clash0
ip route replace default dev clash0 table 0x162
ip rule add fwmark 0x162 lookup 0x162
iptables -t mangle -N CLASH
iptables -t mangle -F CLASH
iptables -t mangle -A CLASH -d 198.18.0.0/16 -j MARK --set-mark 0x162
iptables -t mangle -A CLASH -m addrtype --dst-type BROADCAST -j RETURN
iptables -t mangle -A CLASH -m set --match-set localnetwork dst -j RETURN
iptables -t nat -N CLASH_DNS
iptables -t nat -F CLASH_DNS 
iptables -t nat -A CLASH_DNS -p udp -j REDIRECT --to-port 1053
iptables -t mangle -I OUTPUT -j CLASH
iptables -t mangle -I PREROUTING -m set ! --match-set localnetwork dst -j MARK --set-mark 0x162
iptables -t nat -I OUTPUT -p udp --dport 53 -j CLASH_DNS
iptables -t nat -I PREROUTING -p udp --dport 53 -j REDIRECT --to 1053
iptables -t filter -I OUTPUT -d 172.31.255.253/30 -j REJECT
```

Sekarang mari kita lanjutkan setting ke bagian **Fake IP**.

Langkah awal nya juga sama seperti **Redir Host** namun ada sedikit perbedaan.

```
dns:
  enable: true
  listen: 0.0.0.0:1053
  enhanced-mode: fake-ip
  nameserver:
    - 114.114.114.114

tun:
  enable: true
  device-url: dev://clash0 #specific a TUN device
  dns-listen: 0.0.0.0:1053 #TUN dns listen port, only DNS requires bypassed it, tun can hijack them
```

Untuk routing di linux dan openwrt pun juga ada kesamaan

```
# Based on https://github.com/Kr328/kr328-clash-setup-scripts/blob/master/setup-clash-tun.sh
# Make sure your clash DNS listen at 1053, otherwise you should modify some part

ipset create localnetwork hash:net
ipset add localnetwork 127.0.0.0/8
ipset add localnetwork 10.0.0.0/8
ipset add localnetwork 169.254.0.0/16
ipset add localnetwork 192.168.0.0/16
ipset add localnetwork 224.0.0.0/4
ipset add localnetwork 240.0.0.0/4
ipset add localnetwork 172.16.0.0/12
ip tuntap add user root mode tun utun0
ip link set utun0 up
ip address replace 172.31.255.253/30 dev utun0
ip route replace default dev utun0 table 0x162
ip rule add fwmark 0x162 lookup 0x162
iptables -t mangle -N CLASH
iptables -t mangle -F CLASH
iptables -t mangle -A CLASH -d 198.18.0.0/16 -j MARK --set-mark 0x162
iptables -t mangle -A CLASH -m addrtype --dst-type BROADCAST -j RETURN
iptables -t mangle -A CLASH -m set --match-set localnetwork dst -j RETURN
iptables -t mangle -A CLASH -j MARK --set-mark 0x162
iptables -t nat -N CLASH_DNS
iptables -t nat -F CLASH_DNS 
iptables -t nat -A CLASH_DNS -p udp -j REDIRECT --to-port 1053
iptables -t mangle -I OUTPUT -j CLASH
iptables -t mangle -I PREROUTING -m set ! --match-set localnetwork dst -j MARK --set-mark 0x162
iptables -t nat -I OUTPUT -p udp --dport 53 -j CLASH_DNS
iptables -t nat -I PREROUTING -p udp --dport 53 -j REDIRECT --to 1053
iptables -t filter -I OUTPUT -d 172.31.255.253/30 -j REJECT
```
