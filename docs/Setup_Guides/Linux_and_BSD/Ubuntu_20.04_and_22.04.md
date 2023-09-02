## Overview

The easiest way to set Quad9 on your entire network is via your router settings. If you'd prefer to set Quad9 on a single system, please follow the steps below to configure Ubuntu 22.04 or 22.04 LTS to use Quad9.

!!! warning "Firefox, VPNs"
    * **Firefox** is set to use Cloudflare DNS by default in some regions. If you're using Firefox, check that [this is disabled](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPNs** typically do not respect the system or router-level DNS settings. If you're using a VPN, configure Quad9's IP addresses in the `Custom DNS` settings of your VPN client. Refer to your VPN provider's documentation for further information.

## Instructions

### IPv4 

* From the Ubuntu desktop, select the drop down menu in the top right corner of the screen, expand either `Wired Connection` or `Wireless Connection` based on your connection type, then select `Wired Settings` or `Wireless Settings`.

* Click the :gear: icon next to your connection.

* Click the `IPv4` tab
    * Disable `Automatic DNS`
        * Enter the Quad9 IP addresses of your preferred service.

Multiple IP addresses can be entered in the list using comas.

`9.9.9.9, 149.112.112.112`

* If you will not use IPv6, click `Apply` to complete the setup process, and then confirm you're using Quad9.


### IPv6 (Optional)

If your network/computer support IPv6, it's also recommended to configure the Quad9 IPv6 addresses. If you're not sure if IPv6 is configured on your network, you can test that here: https://test-ipv6.com/


* Select the `IPv6` tab
    * Disable `Automatic DNS`
        * Enter the Quad9 IP addresses of your preferred service.

Multiple IP addresses can be entered in the list using comas.

2620:fe::fe, 2620:fe::9

* Click `Apply` to complete the setup process.

## Verify Configuration

Confirm you're using Quad9.

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
