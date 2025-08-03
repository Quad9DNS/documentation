## Overview

This article describes how to configure and use FreeBSD's pre-installed "local_unbound" service in order to send encrypted DNS via DNS over TLS to Quad9.

This was tested using FreeBSD 14.3 and may not work with prior branches (13.x, etc).

!!! warning "Firefox, VPNs"
    * **Firefox** is set to use Cloudflare DNS by default in some regions. If you're using Firefox, check that [this is disabled](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPNs** typically do not respect the system or router-level DNS settings. If you're using a VPN, configure Quad9's IP addresses in the `Custom DNS` settings of your VPN client. Refer to your VPN provider's documentation for further information.

!!! warning
    FreeBSD, by default, installs a local instance of Unbound DNS. This is meant to act as a local, caching DNS forwarder for the local machine only, and is not intended to act as a DNS forwarder for other network devices. If you want to run Unbound DNS on FreeBSD for the purposes of running a caching DNS forwarder that will be used by multiple devices on the network, FreeBSD recommends installing the dns/unbound package instead. These instructions are only valid for the "local_unbound" service.

## Prerequisites

For simplicity, these instructions require that you are logged in as, or `su`d to the **root** user.

* Install the dig command so you can test DNS resolution is working as expected:

```
pkg install bind-tools
```

* Install the standard root/CA store so Unbound can perform TLS validation of the Quad9 certificate.

```
pkg install ca_root_nss
```

* Verify local_unbound is Enabled

```
grep unbound /etc/rc.conf
```

If the following output is produced, local_unbound is already enabled, and you can skip to the **Instructions** section:

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
local-unbound-setup
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
## Instructions

This command will back up the default configuration files, download the modified config files from the attachment of this article, and restart the local_unbound service.

```
mv /var/unbound/forward.conf /var/unbound/forward-ORIG.conf && mv /var/unbound/unbound.conf /var/unbound/unbound-ORIG.conf && fetch -o /var/unbound/unbound.conf https://docs.quad9.net/assets/conf/freebsd/unbound.conf && fetch -o /var/unbound/forward.conf https://docs.quad9.net/assets/conf/freebsd/forward.conf && service local_unbound restart
```

These files are configured for the 9.9.9.9 service by default, without IPv6. If you'd like to use the .10 or .11 service instead, and/or enable IPv6, open the `/var/unbound/forward.conf` file and un-comment/comment out the appropriate lines.

## Verify Configuration

Using the [Quad9 Protocol test](https://docs.quad9.net/FAQs/#protocol-test-confirm-on-which-protocol-quad9-received-your-query), the result should be `dot.`, which indicates your queries are being sent to Quad9 and are encrypted with DNS over TLS:

```
dig +short txt proto.on.quad9.net.
```

## Undo

To undo the configuration changes to local_unbound, simply run this command to restore the original files and restart local_unbound:

```
mv /var/unbound/forward-ORIG.conf /var/unbound/forward.conf && mv /var/unbound/unbound-ORIG.conf /var/unbound/unbound.conf && service local_unbound restart
```

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
