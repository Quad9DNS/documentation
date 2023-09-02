### Overview

OPNsense is an open-source firewall, used in both consumer and commercial environments.

OPNsense utilizes Unbound, which has built-in DNS over TLS support, with the configuration being accessible in the GUI.

!!! warning "Backup Time!"
    Before making changes to a production environment, we recommend [backing up the existing configuration](https://docs.opnsense.org/manual/backups.html#backup)

### Instructions

* Navigate to `Services` -> `DNS over TLS` on the left-side menu
    * Click the + button
        * Add 4 entries, using `dns.quad9.net` in the **Verify CN** Field, and `853` in the **Server Port:** field.

Server IP: `9.9.9.9`
Server IP: `149.112.112.112`
Server IP: `2620:fe::fe`
Server IP: `2620:fe::9`

!!! warning "IPv6"
    If your network does not have IPv6, which you can test here, then IPv6 addresses should not be added, as it may result in a percentage of your DNS requests failing.

* Click `Apply` to save the changes.

* Navigate to `System` -> `Settings` -> `General` on the left-side menu.

* Disable `Allow DNS server list to be overridden by DHCP/PPP on WAN`
* Click `Save`
* Click `Apply` at the top of the page

### Verify Configuration

To confirm that OPNsense is now sending your queries via DNS over TLS, you can run a packet capture in command line, such as:

```
tcpdump -i em0 'port 853'
```

!!! note
    You may have to adjust the interface name from em0 to that of your device's WAN interface.

You can also test from a macOS, Linux, or Windows system that is connected to this OPNsense router/firewall.

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
