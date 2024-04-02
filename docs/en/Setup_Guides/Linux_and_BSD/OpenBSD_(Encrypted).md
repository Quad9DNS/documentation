## Overview

This article describes how to configure and use Unbound on OpenBSD in order to send encrypted DNS via DNS over TLS to Quad9.

This was tested using OpenBSD 7.1.

!!! warning "Firefox, VPNs"
    * **Firefox** is set to use Cloudflare DNS by default in some regions. If you're using Firefox, check that [this is disabled](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPNs** typically do not respect the system or router-level DNS settings. If you're using a VPN, configure Quad9's IP addresses in the `Custom DNS` settings of your VPN client. Refer to your VPN provider's documentation for further information.

!!! warning
    Unbound DNS is installed by default on standard OpenBSD installations. This is meant to act as a local, caching DNS forwarder for the local machine only, and is not intended to act as a DNS forwarder for other network devices. If you want to run Unbound DNS on OpenBSD for the purposes of running a caching DNS forwarder that will be used by multiple devices on the network, you can modify the interface and access-control values in unbound.conf appropriately, which by default, only allow DNS queries from localhost.

## Instructions

You must be logged in as the root user directly or by running the `su` command and typing in your password in a Terminal session.

* Back up the default unbound.conf file and download the replacement `unbound.conf` file, which is pre-configured for sending DNS queries to Quad9 via DNS over TLS.

!!! note
    You're encouraged to download and inspect the unbound.conf file in a text editor, which is attached to this article, before downloading it to your OpenBSD system.

```
mv /var/unbound/etc/unbound.conf /var/unbound/etc/unbound.BAK && ftp -o /var/unbound/etc/unbound.conf https://docs.quad9.net/assets/conf/openbsd/unbound.conf
```

Optional: If your network supports IPv6, open the /var/unbound/etc/unbound.conf file on OpenBSD with your favorite text editor, and make the following changes, removing the # (comment) before these lines begin.

**Before**

```
# do-ip6: no
# forward-addr: 2620:fe::fe@853#dns.quad9.net
# forward-addr: 2620:fe::9@853#dns.quad9.net
```

**After**

```
do-ip6: yes
forward-addr: 2620:fe::fe@853#dns.quad9.net
forward-addr: 2620:fe::9@853#dns.quad9.net
```

* Set Unbound to start on system startup, and enable the service (run these commands one at a time):

```
rcctl enable unbound
```
```
rcctl start unbound
```

## Verify Configuration

Open a separate/second Terminal session to the OpenBSD system as the root user and start a packet capture, filtering for port 853 (DNS over TLS port):
tcpdump -n 'port 853'

* On your first Terminal session, make sure Unbound can answer DNS queries:
dig +short quad9.net @127.0.0.1

The result should be: 216.21.3.77

On your second Terminal session, tcpdump should show output like this, which confirms that the DNS query was sent to Quad9 with DNS over TLS:
```
tcpdump: listening on em0, link-type EN10MB
00:29:08.307240 192.168.1.194.42064 > 149.112.112.112.853: S 3620809840:3620809840(0) win 16384 <mss 1460,nop,nop,sackOK,nop,wscale 6,nop,nop,timestamp 495425124 0> (DF)
00:29:08.313467 149.112.112.112.853 > 192.168.1.194.42064: S 1684627303:1684627303(0) ack 3620809841 win 28960 <mss 1460,nop,nop,timestamp 3541989193 495425124,nop,wscale 8> (DF)
00:29:08.313559 192.168.1.194.42064 > 149.112.112.112.853: . ack 1 win 256 <nop,nop,timestamp 495425124 3541989193> (DF)
00:29:08.313895 192.168.1.194.42064 > 149.112.112.112.853: P 1:310(309) ack 1 win 256 <nop,nop,timestamp 495425124 3541989193> (DF)
00:29:08.319973 149.112.112.112.853 > 192.168.1.194.42064: . ack 310 win 118 <nop,nop,timestamp 3541989200 495425124> (DF)
00:29:08.320719 149.112.112.112.853 > 192.168.1.194.42064: . 1:1449(1448) ack 310 win 118 
```

Set your system to start using Unbound for DNS by backing up the existing resolv.conf file and set 127.0.0.1 as the DNS server for the system:
```
cp /etc/resolv.conf /etc/resolv.BAK && echo "nameserver 127.0.0.1" > /etc/resolv.conf
```

## Undo

If you want to stop using Unbound as the DNS server, simply restore the backed-up resolv.conf file:

```
mv /etc/resolv.BAK /etc/resolv.conf
```

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
