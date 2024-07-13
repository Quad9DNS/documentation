## Overview

Please follow the steps below to install the Quad9 DNS Profile. Requires iOS 14 or later.

!!! failure "VPNs, iCloud Private Relay, Little Snitch"
    When using iCloud Private Relay, most VPN clients, or Little Snitch, it will not utilize/respect this DNS profile.

    * **VPN**: do not follow these instructions. Instead set Quad9's IP addresses in the `Custom DNS` settings of your VPN client. Refer to your VPN client's documentation for further information.
   
    * **Apple Private Relay**: do not follow these instructions. Apple private relay will use its own DNS servers at the system level, with no way to override it.

## Choosing DNS over TLS or DNS over HTTPS

DNS over HTTPS is recommended for most users. If the device will frequently connect to guest Wi-Fi, and/or networks you do not administrate.

DNS over TLS is recommended only if the device will mainly connect to Wi-Fi networks you control, or on corporate networks where DNS over TLS is allowed.

## Before You Start

!!! note "`nslookup` and `dig`"
    The App Store, as well as the `dig` and `nslookup` commands in a `Terminal` do not use encrypted DNS. This is by design.

!!! warning "DNS over TLS"
    If connected to a Wi-Fi network which blocks DNS over TLS, which may occur on restrictive network firewalls, you will have to disable the profile or disconnect from the network to regain DNS resolution. This solution does not allow for unencrypted "fallback" behavior. DNS over HTTPS is recommended for most users.

!!! warning "This profile will expire!"
    These profiles are only valid until they expire, at which point, they will automatically disable until a new profile is installed. This is by design of Apple, and there is no way around it.

## Download Profile
Download one of the profiles here directly using Safari on your iOS device. You must use Safari to download the file.

**All profiles expire on Jan 29, 2025**

<figure markdown="span">
  ![](https://docs.quad9.net/assets/mobileconfig/mobileconfig_QRreminder_2025_en.png){ width="300" }
  <figcaption>Add a reminder to iCal/Google Calander!</figcaption>
</figure>

[:fontawesome-solid-calendar-days: Add Calendar Event (.ics) :fontawesome-solid-download:](){ .md-button .md-button--primary }

* 9.9.9.9 (DNSSEC, Threat-Blocking)
    * [:fontawesome-solid-star:{ .heart } Recommended: HTTPS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_20250129.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `eeabc4e42bd701e0afc74c9da706024e2df40cca38d9ae3f6be92eaa91986db1`
    * [TLS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_20250129.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `6d826edcf0e7f89c32352266896c8aacd96da8074789d1ecf01f9f60fcc63d8d`

* 9.9.9.10 (No DNSSEC, no Threat-Blocking)
    * [TLS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_20250129.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `cde1057b6dc6f61f73963299a22e7bb2eaa17100cdc60e69896c1f132804859c`
    * [HTTPS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_20250129.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `5dc6b70a7e6d0971a6e988c4f46423d4bdbc66f443d6d92f43c3719675304ea7`

* 9.9.9.11 (DNSSEC, Threat-Blocking, with ECS)
    * [TLS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_ECS_20250129.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `8126f0187de219a0e9df2e2df104df1ffc0f2efa2af3e6d5c441268b3f6a020d`
    * [HTTPS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_ECS_20250129.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `8c9ce407e7032d91252be58c65237d3014710df6622d37d7c0ed40bb80502e70`

* 9.9.9.12 (No DNSSEC, no Threat-Blocking, with ECS)
    * [TLS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_ECS_20250129.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `fe5943d6ad5dd553cf321e7be251cc6da68db1056ab6d754e581c8ab2e3adbb4`
    * [HTTPS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_ECS_20250129.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `79cd0536250e6a1292b318a490057c17d03fd0c90768fad2f999c59b58d89345`

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
