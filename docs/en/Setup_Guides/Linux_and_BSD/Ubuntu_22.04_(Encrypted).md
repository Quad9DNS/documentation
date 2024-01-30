## Overview

Note: The maintainers of systemd-resolved emphasize that this DNS over TLS implementation is currently a work in progress. You may consider using Stubby instead if experiencing performance issues. See here for Ubuntu 18.04 / 20.04 + Stubby instructions.

Ubuntu 22.04 and Linux Mint 20.3 or later support DNS over TLS natively in systemd-resolved, but the option is not available in the GUI.

!!! bug
    While this is technically also supported in Ubuntu *20.04*, we do not recommend using this method for 20.04, since it uses an older systemd-resolve version which has problems. 

!!! bug
    The DNSSEC option should not be enabled in systemd-resolved. It is extremely buggy, and it would only duplicate the DNSSEC validation process which Quad9 already performs, significantly reducing performance.

!!! warning "Firefox, VPNs"
    * **Firefox** is set to use Cloudflare DNS by default in some regions. If you're using Firefox, check that [this is disabled](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPNs** typically do not respect the system or router-level DNS settings. If you're using a VPN, configure Quad9's IP addresses in the `Custom DNS` settings of your VPN client. Refer to your VPN provider's documentation for further information.

## Instructions

* Configure Quad9 in the Network Settings ([Ubuntu](editme), [Linux Mint](editme)).

* Open the `Terminal` application, and copy/paste these commands to enable DNS over TLS. When prompted for your password, type it in and hit `Enter`.

```
sudo sed -i 's/#DNSOverTLS=no/DNSOverTLS=yes/g' /etc/systemd/resolved.conf
```

* Restart the `systemd-resolvd` and `networking services` to recognize the changes to the file:

```
sudo systemctl restart systemd-resolved.service && sudo service network-manager restart
```
## Verify Configuration

* Confirm that DNS over TLS is being used by opening the `Terminal` application and running the following command, typing in your password and pressing `Enter``:

```
$ dig +short txt proto.on.quad9.net.
```
If the response is `dot.`, then it is working! If the response is `do53-udp.`, then it's still using plaintext. If there is no response, that means that Quad9 may not have been configured probably in the `Network Settings`.

## Undo

If you experience any issues or want to undo this configuration change:

* Open the Terminal application, and copy/paste these commands to disable DNS over TLS. You'll be prompted for your password.

```
sudo sed -i 's/DNSOverTLS=yes/#DNSOverTLS=no/g' /etc/systemd/resolved.conf
```

* Restart the `systemd-resolvd` and `networking` services to recognize the changes to the file we just made:

```
sudo systemctl restart systemd-resolved.service && sudo service network-manager restart
```

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
