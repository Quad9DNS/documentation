## Overview

This article describes how to configure and use Unbound on OpenBSD in order to send encrypted DNS via DNS over TLS to Quad9.

This was tested using OpenBSD 7.7.

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

* Set Unbound to start on system startup, and start the service:

```
rcctl enable unbound && rcctl start unbound
```

* Disable resolvd to prevent automatically overriding the `/etc/resolv.conf` file:

```
rcctl disable resolvd && rcctl stop resolvd
```

* Set your system to start using Unbound for DNS by backing up the existing resolv.conf file and set 127.0.0.1 as the DNS server for the system:

```
mv /etc/resolv.conf /etc/resolv.BAK && echo "nameserver 127.0.0.1" > /etc/resolv.conf
```

## Verify Configuration

Using the [Quad9 Protocol test](https://docs.quad9.net/FAQs/#protocol-test-confirm-on-which-protocol-quad9-received-your-query), the result should be `dot.`, which indicates your queries are being sent to Quad9 and are encrypted with DNS over TLS:

```
dig +short txt proto.on.quad9.net.
```

## Undo

If you want to stop using Unbound as the DNS server and revert these changes, simply re-enable/start resolvd:

```
rcctl enable resolvd && rcctl start resolvd
```

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
