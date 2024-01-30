## Overview

The easiest way to set Quad9 on your entire network is via your router settings. If you'd prefer to set Quad9 on a single system, please follow the steps below to configure MX Linux 23 to use Quad9.

!!! warning "Firefox, VPNs"
    * **Firefox** is set to use Cloudflare DNS by default in some regions. If you're using Firefox, check that [this is disabled](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPNs** typically do not respect the system or router-level DNS settings. If you're using a VPN, configure Quad9's IP addresses in the `Custom DNS` settings of your VPN client. Refer to your VPN provider's documentation for further information.

## Instructions

* Right click on the Network/WiFi icon in the system tray on the left side of the screen.
    * Select `Edit Connections`
        * Select your connection Type (Wired or Wi-Fi), then click the :gear: button at the bottom of the window.

* Select the `IPv4 Settings` tab.
    * Change `Method` to `Automatic (DHCP) addresses only`
        * In the `DNS Servers` field, add: `9.9.9.9,149.112.112.112`
            * Click `Save`

## Verify Configuration

Confirm you're using Quad9 by visiting [on.quad9.net](https://on.quad9.net) in your preferred browser.

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
