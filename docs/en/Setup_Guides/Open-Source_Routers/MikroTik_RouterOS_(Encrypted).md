## Overview

This article describes how to configure your MikroTik router using RouterOS to send encrypted DNS queries to Quad9 using DNS over HTTPS.

RouterOS >=6.4.7 is required. These instructions were tested using RouterOS 7.1.3.

!!! warning "Backup Time!"
    Before making changes to a production environment, we recommend [backing up the existing configuration](https://help.mikrotik.com/docs/display/ROS/Backup)

## Instructions

* Connect to your MikroTik router's management interface via SSH or console. The username and password will be the same as if using Webfig (GUI).

* In order for MikroTik to perform certificate verification of the Quad9 DNS over HTTPS domain, we need to download and import the DigiCert Global Root CA certificate.
    * Download the certificate to your MikroTik router:

```
/tool/fetch mode=https url="https://cacerts.digicert.com/DigiCertGlobalG3TLSECCSHA3842020CA1-1.crt.pem"
```

* Import the certificate into the local certificate store. When prompted for a passphrase, just hit enter for no passphrase:

```
/certificate/import file-name=DigiCertGlobalG3TLSECCSHA3842020CA1-1.crt.pem
```

The resulting output should be:

```
passphrase: 
certificates-imported: 1
private-keys-imported: 0
files-imported: 1
decryption-failures: 0
keys-with-no-certificate: 0
```

* Log into Webfig (GUI), and navigate to `IP` -> `DNS` on the left-side menu.
*  In the Servers field, set: `9.9.9.9`, `149.112.112.112`, `2620:fe::fe`, `2620:fe::9`

!!! warning

    If your network does not support IPv6, then the IPv6 addresses should not be added, as it may result in a percentage of your DNS requests failing. Not sure if you have IPv6? [Test here](https://port.tools/ipv6-test/).

*  Use DoH Server: `https://dns.quad9.net/dns-query`
*  Verify DoH Certificate: `Enabled`
*  Allow Remote Requests: `Enabled`

!!! warning

    Don't forget to configure the firewall rules to prevent non-local IP address from using this as a DNS server.

8. Click **Apply** at the top.

### Verify Configuration

To confirm that the MikroTik router is sending DNS queries to Quad9 using DNS over HTTPS, you can use the packet sniffer tool to filter for packets being sent to/from Quad9 IP addresses using port 443 (HTTPS):

```
tool/sniffer/quick port=443 ip-address=9.9.9.9,149.112.112.112
```

If DNS queries sent to the MikroTik router are being forwarded to Quad9 using DNS over HTTPS, you will see any output.

```
Columns: INTERFACE, TIME, NUM, DIR, SRC-MAC, DST-MAC, SRC-ADDRESS, DST-ADDRESS, PROTOCOL, SIZE, CPU
INTERFACE TIME NUM DIR SRC-MAC DST-MAC SRC-ADDRESS DST-ADDRESS PROTOCOL SIZE CPU
ether1 6.886 5 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 66 0
ether1 6.887 6 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 1514 0
ether1 6.887 7 -> 08:00:27:7D:3B:33 04:F0:21:45:C9:0C 192.168.1.222:59348 9.9.9.9:443 (https) ip:tcp 66 0
ether1 6.887 8 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 1514 0
ether1 6.887 9 -> 08:00:27:7D:3B:33 04:F0:21:45:C9:0C 192.168.1.222:59348 9.9.9.9:443 (https) ip:tcp 66 0
```

If you do not yet have endpoints using the MikroTik router for DNS, you can manually query the MikroTik router to facilitate testing and checking for the output generated above from Terminal (Linux/macOS) or Command Prompt (Windows), replacing 192.168.1.1 with the LAN IP address of your MikroTik router.

```
nslookup quad9.net 192.168.1.1
```

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
