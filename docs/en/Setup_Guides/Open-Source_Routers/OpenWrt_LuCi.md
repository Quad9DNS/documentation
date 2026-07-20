## Overview

The OpenWrt Project is a Linux operating system targeting embedded devices, which is often used as an open-source solution for routers and firewalls.

This guide covers setting Quad9 in the DNS forwarder settings. When using your OpenWrt router as a DNS server, it will forward DNS requests to Quad9.

!!! warning "Backup Time!"
    Before making changes to a production environment, we recommend [backing up the existing configuration](https://openwrt.org/docs/guide-user/troubleshooting/backup_restore)

## Instructions

* Log into your LuCI control panel, typically by opening `http://192.168.1.1` in a desktop browser.
* Navigate to `Network` -> `Interfaces`.
* Click `Edit` on the `wan` interface for the IPv4 configuration.
* Uncheck `Use DNS servers advertised` option to reveal the `Use custom DNS servers` fields.
* Add two entries for `9.9.9.9` and `149.112.112.112` by clicking `+` for each additional entry with your preferred Quad9 [service](https://docs.quad9.net/services/).
  * If your network supports IPv6, you can also add `2620:fe::fe` and `2620:fe::9` for the `wan6` interface.
* Click `Save` for each altered interface.
  * Optionally, Navigate to `Network` -> [`DHCP and DNS`](https://openwrt.org/docs/guide-user/base-system/dhcp?s[]=resolv&s[]=file#dhcp_and_dns_configurationetcconfigdhcp) -> `Resolv and Hosts Files` sub-tab, and ensure `Ignore resolv file` is `Enabled`.
* Click `Save & Apply` at the bottom. _Note that your devices may very briefly lose connection._

_Note: See the Official OpenWrt section on "[Interface configuration](https://openwrt.org/docs/guide-user/network/wan/multiwan/mwan3?s[]=quad9#interface_configuration)" for more details._

## Verify Configuration

* [Confirm](https://on.quad9.net/) you're using Quad9 on Linux, MacOS, or Windows.

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
