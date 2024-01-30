## Overview

The easiest way to set Quad9 on your entire network is via your router settings. If you'd prefer to set Quad9 on an individual Windows device, please follow the steps below to configure Windows 11 to use Quad9.

!!! warning "Firefox, VPNs"
    * **Firefox** is set to use Cloudflare DNS by default in some regions. If you're using Firefox, check that [this is disabled](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPNs** typically do not respect the system or router-level DNS settings. If you're using a VPN, configure Quad9's IP addresses in the `Custom DNS` settings of your VPN client. Refer to your VPN provider's documentation for further information.
    

## Instructions

### IPv4

* Right click the Network or WiFi icon on the system tray, and left click `Network and Internet Settings`

* Select `Ethernet` or `WiFi`, depending on your connection type.

* Scroll down and click `Edit` next to `DNS server assignment`

* Make the following changes:
    * Change `Automatic (DHCP)` to `Manual`
    * Toggle the `On` switch to change the DNS server
    * Enter into `Preferred DNS`: 9.9.9.9
        * Set `Preferred DNS encryption` to `Encrypted Only (DNS over HTTPS)`
    * Enter into `Alternate DNS`: 149.112.112.112
        * Set Alternate DNS encryption to Encrypted Only (DNS over HTTPS)
!!! note
    If using a laptop that roams to other networks which may block DNS over HTTPS, consider choosing `Encryption preferred, unencrypted allowed` instead of `Encrypted Only`.

* Click `Save`

### IPv6
If using IPv6, which you can confirm here, you should also scroll down and set up Quad9 on IPv6.
Note: if Windows is not configured with an IPv6 address, setting up an IPv6 DNS server could cause DNS resolution to fail.

## Verify Configuration

* Open the Terminal application, and execute this command:

```
Resolve-DnsName -Type txt proto.on.quad9.net.
```

The output should show `doh.` (DNS over HTTPS) in the `NameHost` section if you set Quad9 in the Network Settings and enabled encryption.

```
Name                           Type   TTL   Section    NameHost
----                           ----   ---   -------    --------
proto.on.quad9.net             CNAME  60    Answer     doh
```

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
