Customized OpenWRT Feed
=======================

Developers simply use
---------------------

```shell
cp ./feeds.conf.default  ./feeds.conf
echo "src-git hc_packages https://github.com/cj1324/hc_openwrt_packages.git" >>./feeds.conf
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make -j2
```

[Official Documents](http://wiki.openwrt.org/doc/devel/feeds "Official Documents")

Features
--------

+ Additions and improvements shadowsocks-libev (Improved compatibility with firewall rules)
+ Custom ipset version dnsmasq (Does not include ipv6, DNSSEC)
+ chinadns use [fork me](https://github.com/cj1324/ChinaDNS-OpenWRT "Github") (without chnroute)
+ Instead of the official svn oldpackages (My personal customization)

Package List
------------

+ net

  + axel
  + chinadns `^`
  + dnsmasq-ipset `^`
  + iptraf
  + shadowsocks-libev `^`
  + socat

+ devel

  + diffutils

+ utils

  + mksh
  + procps
  + vim

> Marked improvement project
