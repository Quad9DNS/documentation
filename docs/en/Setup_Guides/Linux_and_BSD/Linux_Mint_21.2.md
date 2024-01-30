## Overview

The easiest way to set Quad9 on your entire network is via your router settings. If you'd prefer to set Quad9 on a single system, please follow the steps below to configure Linux Mint to use Quad9.

!!! warning "Firefox, VPNs"
    * **Firefox** is set to use Cloudflare DNS by default in some regions. If you're using Firefox, check that [this is disabled](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPNs** typically do not respect the system or router-level DNS settings. If you're using a VPN, configure Quad9's IP addresses in the `Custom DNS` settings of your VPN client. Refer to your VPN provider's documentation for further information.

## Instructions 

* Click the `Network` or `Wi-Fi` icon on the system tray in the bottom-right corner.
    * Click `Network Settings`
        * Click the :gear: icon on the bottom-right corner of the dialogue window.
### IPv4

* Select `IPv4` on the left-side menu.
    * In the `DNS` section:
        * Disable `Automatic`
            * Click the :plus: botton to add a second `Server` field.
                * Enter `9.9.9.9` in the first `Server` field, and `149.112.112.112` in the second.
                    * Click `Apply`

## Verify Configuration

Confirm you're using Quad9 by visiting [on.quad9.net](https://on.quad9.net) in your preferred browser.

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
