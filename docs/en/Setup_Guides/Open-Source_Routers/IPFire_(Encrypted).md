## Overview

IPFire is an open-source firewall and router, used in both consumer and commercial environments.

IPFire utilizes Unbound, which has built-in DNS over TLS support, with the configuration being accessible in the GUI.

This setup guide was tested using IPFire 2.27

!!! warning "Backup Time!"
    Before making changes to a production environment, we recommend [backing up the existing configuration](https://wiki.ipfire.org/configuration/system/backup)

## Instructions

* Navigate to `System` -> `Domain Name System`
    * Under `DNS Servers`, click `Add`
        * Go through this process twice, one for each Quad9 IP address, where the TLS Hostname will always be dns.quad9.net
            * IP address: `9.9.9.9`
            * IP address: `149.112.112.112`

* Use ISP-assigned DNS Servers: `Disabled`
* Protocol for DNS Queries: `TLS`
* Enable Safe Search: `Disabled`
* QNAME Minimisation: `Disabled`
* Click `Save`

## Verify Configuratiom

### GUI

Navigate to `Status` -> `Net-Traffic` in the top menu, and search for an active connect to either `9.9.9.9` or `149.112.112.112` via port 853 TCP

### CLI

* Connect to your IPFire device via SSH
* Install the tshark package

```
pakfire -y install tshark
```

* Start a packet capture with tshark to filter for DNS over TLS traffic:

```
tshark -i any 'port 853'
```

If the IPFire device is using DNS over HTTPS for DNS queries, you will see output like this:
```
1 0.000000000 192.168.1.150 → 9.9.9.9 TCP 76 37226 → 853 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM=1 TSval=3103990808 TSecr=0 WS=512
2 0.006914259 9.9.9.9 → 192.168.1.150 TCP 76 853 → 37226 [SYN, ACK] Seq=0 Ack=1 Win=28960 Len=0 MSS=1460 TSval=2447463919 TSecr=3103990808 WS=256
3 0.006948874 192.168.1.150 → 9.9.9.9 TCP 68 37226 → 853 [ACK] Seq=1 Ack=1 Win=64512 Len=0 TSval=3103990815 TSecr=2447463919
4 0.007110658 192.168.1.150 → 9.9.9.9 TLSv1 387 Client Hello
5 0.013306457 9.9.9.9 → 192.168.1.150 TCP 68 853 → 37226 [ACK] Seq=1 Ack=320 Win=30208 Len=0 TSval=2447463926 TSecr=3103990815
6 0.013926633 9.9.9.9 → 192.168.1.150 TLSv1.3 2964 Server Hello, Change Cipher Spec, Application Data
7 0.013945067 192.168.1.150 → 9.9.9.9 TCP 68 37226 → 853 [ACK] Seq=320 Ack=2897 Win=62464 Len=0 TSval=3103990822 TSecr=2447463926
```

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
