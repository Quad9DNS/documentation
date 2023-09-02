## Overview

The easiest way to set Quad9 on your entire network is via your router settings. If you'd prefer to set Quad9 on an individual Windows device, please follow the steps below to configure Windows 10 to use Quad9.

!!! warning "Firefox, VPNs"
    * **Firefox** is set to use Cloudflare DNS by default in some regions. If you're using Firefox, check that [this is disabled](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPNs** typically do not respect the system or router-level DNS settings. If you're using a VPN, configure Quad9's IP addresses in the `Custom DNS` settings of your VPN client. Refer to your VPN provider's documentation for further information.

## Instructions

### IPv4

* Right click on the Network icon (Wired or WiFi) in the system tray and click `Open Network & Internet Settings`.

* Click `Change adapter options`

* Select `Properties`.

* Select `Internet Protocol Version 4 (TCP/IPv4)`. Then, click `Properties`.

* Select `Use the following DNS server addresses`.
    * Enter: `9.9.9.9` in Preferred DNS Server
    * Enter: `149.112.112.112` in Alternate DNS Server.
* Click `OK`.

### IPv6

If your networks supports IPv6, it's also recommended to configure the Quad9 IPv6 addresses. If you're not sure if IPv6 is configured on your network, you can test that here: https://test-ipv6.com/


Select Internet Protocol Version 6 (TCP/IPv6).  Then click Properties.

Select Use the following DNS server addresses.
Enter: 2620:fe::fe in Preferred DNS Server
Enter: 2620:fe::9 in Alternate DNS Server.
Click OK.

## Verify Configuration

Close all configuration boxes.  You should be using Quad9. To confirm you're using Quad9, please see How to Confirm You're Using Quad9 - Windows

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
