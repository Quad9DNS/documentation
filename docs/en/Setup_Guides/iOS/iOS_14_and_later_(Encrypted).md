## Overview

Please follow the steps below to install the Quad9 DNS Profile. Requires iOS 14 or later.

!!! failure "VPNs, iCloud Private Relay, Little Snitch"
    When using iCloud Private Relay, most VPN clients, or Little Snitch, it will not utilize/respect this DNS profile.

    * **VPN**: do not follow these instructions. Instead set Quad9's IP addresses in the `Custom DNS` settings of your VPN client. Refer to your VPN client's documentation for further information.
   
    * **Apple Private Relay**: do not follow these instructions. Apple private relay will use its own DNS servers at the system level, with no way to override it.

## TLS vs HTTPS

DNS over HTTPS is recommended for most users. If the device will frequently connect to guest Wi-Fi and/or networks you do not administrate. HTTPS has a minuscule chance of being blocked on firewalls.

DNS over TLS is recommended only if the device will mainly connect to Wi-Fi networks you control, or on corporate networks where DNS over TLS is allowed. TLS has a higher chance of being blocked on firewalls.

## Before You Start

!!! note "`nslookup` and `dig`"
    The App Store, as well as the `dig` and `nslookup` commands in a `Terminal` do not use encrypted DNS. This is by design.

!!! warning "DNS over TLS"
    If connected to a Wi-Fi network which blocks DNS over TLS, which may occur on restrictive network firewalls, you will have to disable the profile or disconnect from the network to regain DNS resolution. This solution does not allow for unencrypted "fallback" behavior. DNS over HTTPS is recommended for most users.

!!! warning "Profiles expire on January 29th, 2027!"
    These profiles are only valid until they expire, at which point, they will automatically disable until a new profile is installed. This is by design of Apple, and there is no way around it.

    Remind yourself to download a new version a few days before they expire by adding a calendar event.

## Download Profile
Download one of the profiles here directly using :fontawesome-brands-safari: Safari on your iOS device. This will not work if downloaded with a different browser.

* 9.9.9.9 (DNSSEC, Threat-Blocking)
    * [:fontawesome-solid-star:{ .heart } Recommended: HTTPS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `2fd22c5ca55ba2404a63f28a9cb4e25545194989a929895b3a689be232e62871`
    * [TLS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `56af33fe8d1e0f55d429f826fa9822a0a97a8aeb7ad28cca82b26536753d8132`

* 9.9.9.10 (No DNSSEC, no Threat-Blocking)
    * [HTTPS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `ef18da540f7c30a3e9e0e7c4a40c3cde29791da0e02b9851f0195099383c901f`
    * [TLS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `6a76af77beace68de0a3ad3b4847eeff3f90eca60a2a7a01fd3063f2366f764c`

* 9.9.9.11 (DNSSEC, Threat-Blocking, with ECS)
    * [HTTPS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `1212594f9919783167338ea7d1797e8532e4b1426d58e0324983499c8c68dfc2`
    * [TLS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `43a8da875650c899ce8ba6005040fca520951803bd9a02141ef7815cd164f785`

* 9.9.9.12 (No DNSSEC, no Threat-Blocking, with ECS)
    * [HTTPS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `f5b2d174c7096b976af1c59df9c2423126ef59d96ae3fa2a8a3138907f910f2d`
    * [TLS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `beb4610573f73d5fb524594530f07107000eb352b804f39ef84b226a8b75ab85`

## Installation

* Navigate to your Downloads folder and select to the profile you just downloaded.
    * Open `Settings` > `Profile Downloaded` and select the Quad9 profile you opened.
        * Click `Install`.
            * Enter your phone's passcode.
!!! note
    You will receive a warning message warning that your network traffic may be filtered or monitored by the DNS server. While Quad9’s profile can protect your device by filtering potentially malicious traffic, none of your traffic will be logged by Quad9. Please refer to our [Privacy Policy](https://quad9.net/service/privacy) for more information.

* Select `Install`, then `Install` again.

* The profile is now installed. Select `Done`.

## Verify Configuration

To confirm the installation was successful, visit [on.quad9.net](https://on.quad9.net)

Questions? Issues? Didn't work? Contact us!

[Get Support :fontawesome-solid-arrow-up-right-from-square:](https://quad9.net/support/contact){ .md-button .md-button--primary }
