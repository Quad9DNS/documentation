## Overview

Android 9 and later includes the `Private DNS` feature, which allows you to connect to DNS servers using DNS over TLS (DoT). It is important to note, that the private DNS function does not work if the Quad9 Connect app is installed and enabled. To configure your Android device to use Quad9 in this way, follow the steps below.

!!! warning "VPNs"
    The Private DNS feature will not be utilized if you are using a VPN. If using a VPN, instead, configure Quad9's IP addresses in your VPN's `Custom DNS` settings. Please refer to your VPN provider's documentation fr more information

## Instructions

* Open the :material-cog: `Settings` app on your Android device.
    * Select :material-wifi: ` Network & Internet`.
        * Select `Private DNS`.

* Select `Private DNS provider hostname`
    * Enter: `dns.quad9.net`
        * Press `Save`

## Verify Configuration

Visit [on.quad9.net](https://on.quad9.net) in your browser of choice.

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
