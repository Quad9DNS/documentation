## Overview

This article describes how to configure and use FreeBSD's pre-installed "local_unbound" service in order to send encrypted DNS via DNS over TLS to Quad9.

This was tested using FreeBSD 13.1, but should work with 12.X as well.

!!! warning "Firefox, VPNs"
    * **Firefox** is set to use Cloudflare DNS by default in some regions. If you're using Firefox, check that [this is disabled](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPNs** typically do not respect the system or router-level DNS settings. If you're using a VPN, configure Quad9's IP addresses in the `Custom DNS` settings of your VPN client. Refer to your VPN provider's documentation for further information.

!!! warning
    FreeBSD, by default, installs a local instance of Unbound DNS. This is meant to act as a local, caching DNS forwarder for the local machine only, and is not intended to act as a DNS forwarder for other network devices. If you want to run Unbound DNS on FreeBSD for the purposes of running a caching DNS forwarder that will be used by multiple devices on the network, FreeBSD recommends installing the dns/unbound package instead. These instructions are only valid for the "local_unbound" service.

## Instructions

You will need the sudo command to run the commands below. Alternatively, you can simply use the su command to become the root user and execute these commands directly as the root user, in which case, you'll need to remove "sudo" from all the commands below.

* Install the dig command so you can test DNS resolution is working as expected:

```
pkg install bind-tools
```

* Verify local_unbound is Enabled

```
sudo grep unbound /etc/rc.conf
```

If the following output is produced, local_unbound is already enabled, and you can skip to the next section:

```
local_unbound_enable="YES"
```

* If there is no output after this command, then local_unbound must be enabled.
    * Tell the system that we want to use local_unbound:
```
echo 'local_unbound_enable="YES"' >> /etc/rc.conf
```

Then reboot the system (yes, really):

```
reboot
```

* Enable local_unbound:

```
sudo local-unbound-setup
```

The output should similar to this, but may differ slightly:

```
destination: 
Extracting forwarders from /etc/resolv.conf.
/var/unbound/forward.conf not modified
/var/unbound/lan-zones.conf not modified
/var/unbound/control.conf not modified
/var/unbound/unbound.conf not modified
local_unbound not running? (check /var/run/local_unbound.pid).
Starting local_unbound.
/etc/resolvconf.conf created
Original /etc/resolv.conf saved as /var/backups/resolv.conf.20220625.200835
```

Configuring local_unbound for DNS over TLS to Quad9

This command will back up the default configuration files, download the modified config files from the attachment of this article, and restart the local_unbound service.

```
sudo mv /var/unbound/forward.conf /var/unbound/forward-ORIG.conf && sudo mv /var/unbound/unbound.conf /var/unbound/unbound-ORIG.conf && sudo fetch -o /var/unbound/unbound.conf https://docs.quad9.net/assets/conf/freebsd/unbound.conf && sudo fetch -o /var/unbound/forward.conf https://docs.quad9.net/assets/conf/freebsd/forward.conf && sudo service local_unbound restart
```

These files are configured for our 9.9.9.9 service by default, without IPv6. If you'd like to use the .10 or .11 service instead, and/or enable IPv6, open the `/var/unbound/forward.conf` file and un-comment/comment out the appropriate lines.

## Verify Configuration

You'll need two Terminal sessions/windows

In the first session, start a packet capture to filter for DNS over TLS traffic:

```
sudo tcpdump -n 'port 853'
```

In the second session, generate some DNS lookups:

```
dig +short quad9.net && dig +short www.quad9.net && dig +short zombo.com
```

Refer back to the first session. If you see any output, your system is now using DNS over TLS to send encrypted DNS to Quad9:

```
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on em0, link-type EN10MB (Ethernet), capture size 262144 bytes
20:30:21.004625 IP 192.168.1.118.29017 > 149.112.112.112.853: Flags [S], seq 255439876, win 65535, options [mss 1460,nop,wscale 6,sackOK,TS val 2441683586 ecr 0], length 0
20:30:21.011088 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [S.], seq 838572319, ack 255439877, win 28960, options [mss 1460,nop,nop,TS val 3171725219 ecr 2441683586,nop,wscale 8], length 0
20:30:21.011140 IP 192.168.1.118.29017 > 149.112.112.112.853: Flags [.], ack 1, win 1027, options [nop,nop,TS val 2441683592 ecr 3171725219], length 0
20:30:21.011628 IP 192.168.1.118.29017 > 149.112.112.112.853: Flags [P.], seq 1:294, ack 1, win 1027, options [nop,nop,TS val 2441683592 ecr 3171725219], length 293
20:30:21.017885 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [.], ack 294, win 118, options [nop,nop,TS val 3171725226 ecr 2441683592], length 0
20:30:21.018447 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [.], seq 1:1449, ack 294, win 118, options [nop,nop,TS val 3171725227 ecr 2441683592], length 1448
20:30:21.018453 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [.], seq 1449:2897, ack 294, win 118, options [nop,nop,TS val 3171725227 ecr 2441683592], length 1448
```

## Undo

To undo the configuration changes to local_unbound, simply run this command to restore the original files and restart local_unbound:

```
sudo mv /var/unbound/forward-ORIG.conf /var/unbound/forward.conf && sudo mv /var/unbound/unbound-ORIG.conf /var/unbound/unbound.conf && sudo service local_unbound restart
```

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
