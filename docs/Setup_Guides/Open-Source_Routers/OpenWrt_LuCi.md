## Overview

The OpenWrt Project is a Linux operating system targeting embedded devices, which is often used as an open-source solution for routers and firewalls.

This guide covers setting Quad9 in the DNS forwarder settings. When using your OpenWrt router as a DNS server, it will forward DNS requests to Quad9.

!!! warning "Backup Time!"
    Before making changes to a production environment, we recommend [backing up the existing configuration](https://openwrt.org/docs/guide-user/troubleshooting/backup_restore)

## Instructions

* Log into your LuCI control panel, typically by opening `http://192.168.1.1` in your browser.

* Navigate to `Network` -> `DHCP and DNS`
    * Set `9.9.9.9` and `149.112.112.112`, or the addresses of your preferred Quad9 service in the "DNS forwardings" input fields.

* If your network supports IPv6, you can also add 2620:fe::fe and 2620:fe::9, or the IPv6 addresses of your preferred Quad9 service.

* Navigate to `Resolv and Hosts Files` sub-tab, and make sure `Ignore resolv file` is `Enabled`.

* Click `Save & Apply` at the bottom. Since you are not changing the DHCP settings, the change should be instantaneous .

## Verify Configuration

* Confirm you're using Quad9 on Linux, MacOS, or Windows.

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
