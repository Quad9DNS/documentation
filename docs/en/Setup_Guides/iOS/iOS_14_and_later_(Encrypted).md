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

!!! warning "Profiles expire on January 29th, 2025!"
    These profiles are only valid until they expire, at which point, they will automatically disable until a new profile is installed. This is by design of Apple, and there is no way around it.

    Remind yourself to download a new version a few days before they expire by adding a calendar event:
    
    [:fontawesome-solid-calendar-days: Add Calendar Event (.ics) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_MobileConfig2025_en.ics){ .md-button .md-button--primary }

## Download Profile
Download one of the profiles here directly using :fontawesome-brands-safari: Safari on your iOS device. This will not work if downloaded with a different browser.

* 9.9.9.9 (DNSSEC, Threat-Blocking)
    * [:fontawesome-solid-star:{ .heart } Recommended: HTTPS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `b240f046a16f7d0e5df6458f5121221c4f118bf4d415cd8cce47d10b6fd46d36`
    * [TLS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `d132d71447bc3b43e371a86533e4d12fa46a4690a63abf77b2ceae72a1b3cef3`

* 9.9.9.10 (No DNSSEC, no Threat-Blocking)
    * [HTTPS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `42cb9445417dc81ced18c33d943c23559a81afb018d440bf465bb0635a44bb66`
    * [TLS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `86588f6d2dac42d03b155c7f557b4dd05b354059736aaa4ec8f3ef4d3ca2548e`

* 9.9.9.11 (DNSSEC, Threat-Blocking, with ECS)
    * [HTTPS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `38c52f0755c4ec053c685e1ebf3b9956841a81373df2cc2e9dc962a418ac6993`
    * [TLS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `abf69de093831cf8c4d644d234a3a594d13026415533ad1bb2b9f1540f307a46`

* 9.9.9.12 (No DNSSEC, no Threat-Blocking, with ECS)
    * [HTTPS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `eccb63252a1cd6726d42a1d72c58e11503cf06a0de6977d2472386f9cc88d9d8`
    * [TLS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `0b01df454c9e4ee7f39b0a79e63920c6fa6e44f1fe17c0064bb8da6ce68bcb04`

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
