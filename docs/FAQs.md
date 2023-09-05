## How Do I Confirm I'm Using Quad9?

The simplest test is to open [on.quad9.net](https://on.quad9.net) in your browser of choice.

## Detecting DNS Transparent Redirection (Hijacks)

Some ISPs, most often in Asia, Africa, or the Middle East, will transparently redirect DNS requests destined for third-party DNS services, like Quad9, to their own DNS forwarders/servers. This may be an attempt to enforce local policies/laws, or to simply increase their cache HIT rate on their DNS forwarders.

You can detect a transparent DNS redirection by executing the following command from the Command Prompt or Terminal of any operating system. If the answer is anything except `resXXX.xxx.rrdns.pch.net`, then DNS is being transparently redirected.

=== "Windows (PowerShell)"

    ```
    nslookup -q=txt -class=chaos id.server. 9.9.9.9 | Select-String "pch"
    ```

=== "MacOS/Linux/BSD (Terminal)"
    ```
    dig +short ch txt id.server. @9.9.9.9
    ```
If the output does not look similar to the following, or there is no output, then DNS is being transparently redirected.

=== "Windows (PowerShell)"
    ```
    Non-authoritative answer:
    "res200.vie.rrdns.pch.net"
    ```

=== "MacOS/Linux/BSD (Terminal)"
    ```
    "res860.qfra3.rrdns.pch.net"
    ```
### My ISP is transparently redirecting DNS. Now what?

Please refer to our Setup Guides appended with `(Encrypted)` in the title. By using encrypted DNS, transparent DNS redirection will not be possible.

## What is EDNS Client Subnet (ECS)?

Quad9's `9.9.9.11` service supports ECS.

EDNS Client Subnet (ECS) allows Quad9 to send a portion of your IP address to authoritative name servers, which helps major content providers (CDNs), such as Google, Microsoft, etc, accurately determine your geolocation.

ECS will have no effect on which Quad9 location your queries are sent to, it simply effects what information Quad9 forwards to the authoritative name server and may effect what IP address they return back. Quad9 uses anycast addressing to ensure you are routed to the nearest Quad9 location available to you regardless of whether or not you use our ECS service.

Since ECS does not play any role in determining where your queries are sent to, it does not have any positive or negative effect on the round trip time (ping) to Quad9

ECS can be viewed as a trade off between privacy and getting geospecific content. One option for the privacy focused user is to leave it disabled and only enable it if you notice a specific domain not delivering you the correct content or not loading at all.

## Network Providers / DNS Leak Tests

Quad9 utilizes multiple network providers in our global network. When running a DNS leak test, it's expected to see IP addresses owned by the following providers:

!!! note "Recommended DNS Leak Test Tool"
    [dnscheck.tools](https://dnscheck.tools/)

* WoodyNet (AKA PCH.net)
* PCH.net
* GSL Networks
* i3D
* EdgeUno
* Equinix Metal (FKA: Packet, Packet.net, or Packethost)
* Path Networks

These organizations are also listed on the Sponsors page of the Quad9 website: [quad9.net/about/sponsors](https://quad9.net/about/sponsors)

If you are trying to simply determine if you are using Quad9, you can visit [on.quad9.net](https://on.quad9.net) instead of relying on a DNS leak test. However, a DNS leak test can be useful to ensure you're exclusively using Quad9, which is required to ensure that all of your DNS requests will be protected by Quad9.
