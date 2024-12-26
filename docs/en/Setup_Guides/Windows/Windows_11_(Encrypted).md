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
    * Toggle the `On` switch under `IPv4` to change the DNS server
    * Enter into `Preferred DNS`: 9.9.9.9
        * Set `DNS over HTTPS` to `On (automatic template)`
    * Enter into `Alternate DNS`: 149.112.112.112
        * Set `DNS over HTTPS` to `On (automatic template)`
!!! note
    If using a laptop that roams to other networks which may block DNS over HTTPS, consider toggling the `Fallback to plaintext` switch.

* Click `Save`

### IPv6
If using IPv6, which you can confirm here: https://test-ipv6.com/, you should also scroll down and set up Quad9 on IPv6.

* Make the following changes:
    * Toggle the `On` switch under `IPv6` to change the DNS server
    * Enter into `Preferred DNS`: 2620:fe::fe
        * Set `DNS over HTTPS` to `On (automatic template)`
    * Enter into `Alternate DNS`: 2620:fe::9
        * Set `DNS over HTTPS` to `On (automatic template)`
!!! note
    If Windows is not configured with an IPv6 address, setting up an IPv6 DNS server could cause DNS resolution to fail.
    If using a laptop that roams to other networks which may block DNS over HTTPS, consider toggling the `Fallback to plaintext` switch.

* Click `Save` 

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
