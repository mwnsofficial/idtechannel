---
layout: post
title:  "Cara mengendalikan port 53 secara manual"
author: Muhammad Yusuf
categories: [ clash ]
image: assets/images/3.jpg
---
Terkadang kita tidak dapat mendengarkan port 53, dan kemudian kita perlu memaksa paket yang ditujukan untuk port 53 ke TUN dari mode clash TUN 2.

> ℹ Tes hanya pada Router dengan OpenWRT

Langkah 1: Edit konfigurasi

Tambahkan bidang tun ke config.yaml

<pre><code class="language-html">
dns:
  enable: true
  listen: 0.0.0.0:7874
  enhanced-mode: fake-ip
  nameserver:
    - 114.114.114.114

tun:
  enable: true
  device-url: dev://clash0 #specific a TUN device
  dns-listen: 0.0.0.0:7874 #TUN dns listen port, only DNS requires bypassed it, tun can hijack them
</code></pre>

Langkah 2: Untuk memulai dan setting anda bisa masuk ke artikel **Redir Host** dan **Fake IP**

Langkah 3: Kendalikan port 53 secara manual

- Umum
<pre><code class="language-html">
uci -q delete firewall.dns_int
uci set firewall.dns_int="redirect"
uci set firewall.dns_int.name="Intercept-DNS"
uci set firewall.dns_int.src="lan"
uci set firewall.dns_int.dest='wan'
uci set firewall.dns_int.src_dport="53"
uci set firewall.dns_int.dest_port="7874"
uci set firewall.dns_int.family="ipv4"
uci set firewall.dns_int.proto="tcp udp"
uci set firewall.dns_int.target="DNAT"
uci commit firewall
/etc/init.d/firewall restart
</code></pre>

- Perutean satu WAN
<pre><code class="language-html">
uci -q delete firewall.dns_int
uci set firewall.dns_int="redirect"
uci set firewall.dns_int.name="Intercept-DNS"
uci set firewall.dns_int.src="wan"
uci set firewall.dns_int.dest='wan'
uci set firewall.dns_int.src_dport="53"
uci set firewall.dns_int.dest_port="7874"
uci set firewall.dns_int.family="ipv4"
uci set firewall.dns_int.proto="tcp udp"
uci set firewall.dns_int.target="DNAT"
uci commit firewall
/etc/init.d/firewall restart
</code></pre>

- Perutean satu LAN
<pre><code class="language-html">
uci -q delete firewall.dns_int
uci set firewall.dns_int="redirect"
uci set firewall.dns_int.name="Intercept-DNS"
uci set firewall.dns_int.src="lan"
uci set firewall.dns_int.dest='lan'
uci set firewall.dns_int.src_dport="53"
uci set firewall.dns_int.dest_port="7874"
uci set firewall.dns_int.family="ipv4"
uci set firewall.dns_int.proto="tcp udp"
uci set firewall.dns_int.target="DNAT"
uci commit firewall
/etc/init.d/firewall restart
</code></pre>
