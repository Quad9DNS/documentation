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

!!! note
    If you do not know which file to choose, we recommend **DNS over HTTPS - 9.9.9.9 (DNSSEC, Threat-Blocking)**

* 9.9.9.9 (DNSSEC, Threat-Blocking)
    * [DNS over TLS - 9.9.9.9](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_20250129.mobileconfig) (Expires Jan 29, 2025)
    * [DNS over HTTPS - 9.9.9.9](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_20250129.mobileconfig) (Expires Jan 29, 2025)

* 9.9.9.10 (No DNSSEC, no Threat-Blocking) (Expires Feb 1st, 2024)
    * [DNS over TLS - 9.9.9.10](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_20250129.mobileconfig) (Expires Jan 29, 2025)
    * [DNS over HTTPS  - 9.9.9.10](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_20250129.mobileconfig) (Expires Jan 29, 2025)

* 9.9.9.11 (DNSSEC, Threat-Blocking, with ECS)
    * [DNS over TLS - 9.9.9.11](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_ECS_20250129.mobileconfig) (Expires Jan 29, 2025)
    * [DNS over HTTPS - 9.9.9.11](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_ECS_20250129.mobileconfig) (Expires Jan 29, 2025)

* 9.9.9.12 (No DNSSEC, no Threat-Blocking, with ECS)
    * [DNS over TLS - 9.9.9.12](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_ECS_20250129.mobileconfig) (Expires Jan 29, 2025)
    * [DNS over HTTPS - 9.9.9.12](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_ECS_20250129.mobileconfig) (Expires Jan 29, 2025)

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

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
