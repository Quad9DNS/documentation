## Quad9, DNS, and VPNs

The vast majority of VPN clients do not utilize the DNS servers assigned in DHCP (by the router) or configured in the local system settings.

If using a VPN, whether sometimes or permanently, and it's desired to utilize Quad9 while the VPN is enabled, it will be required to configure the Quad9 IP addresses in the "Custom DNS" settings of the VPN client. Most, but not all, VPN clients have this functionality, and the exact instructions will vary depending on the client. Please refer to the VPN client's documentation and/or support resources.

If using a VPN, please keep this in mind before running the `on.quad9.net` or protocol tests below.

Configuring Quad9 in a VPN, when the VPN is enabled, also implies that the connection between the client and Quad9 will not be encrypted by DNS over HTTPs or DNS over TLS, regardless if the router or device has DNS over TLS or DNS over HTTPS enabled locally.

## How Do I Confirm I'm Using Quad9?

The simplest test is to open [on.quad9.net](https://on.quad9.net) in your browser of choice.

## Protocol Test - Confirm on which Protocol Quad9 received your query

Confirm which protocol is used when Quad9 receives your DNS queries. This is particularly relevant after setting up DNS encryption, such as DNS over TLS or DNS over HTTPS, in the operating system, router, DNS forwarder.

Execute the following command and refer to the possible responses below:

=== "Windows (PowerShell/Terminal)"

    `Resolve-DnsName -Type txt proto.on.quad9.net.`
=== "MacOS/Linux/Unix (Terminal)"

    `dig +short txt proto.on.quad9.net.`

Possible Responses:

* do53-udp (53/UDP - Plaintext)
* do53-tcp (53/TCP - Plaintext)
* doh (443/TCP - DNS over HTTPS)
* dot (853/TCP - DNS over TLS)
* dnscrypt-udp (UDP - DNSCrypt)
* dnscrypt-tcp (TCP - DNSCrypt)

If you do not receive a response (NXDOMAIN), then Quad9 was not used to perform this DNS query.

## Identifying a Quad9 block

The quickest way to see if a domain is blocked at Quad9 is using our [Blocked Domain Tester](https://quad9.net/result).

When Quad9 blocks a domain, the response is `NXDOMAIN`. `NXDOMAIN` is also returned when a domain does not exist.To differentiate between domains that are nonexistent, and domains that are blocked, we set the `AUTHORITY` value differently.  When you receive an `NXDOMAIN` with `AUTHORITY: 0`, that is a block from Quad9. When you receive `NXDOMAIN` *with* `AUTHORITY: 1`, then that is a domain that does not exist.

A domain will also fail to resolve if DNSSEC authentication fails, but that will result in the `SERVFAIL` code instead of `NXDOMAIN`.

=== "Blocked domain"

    `dig @9.9.9.9 isitblocked.org | grep "status\|AUTHORITY"`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 29193
    ;; flags: qr rd ad; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1
    ```
=== "Nonexistent domain"

    `dig @9.9.9.9 sfaisofnadgre.odafds | grep "status\|AUTHORITY:"`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 22595
    ;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1
    ```
=== "DNSSEC Failure"
    
    `dig @9.9.9.9 A brokendnssec.net +dnssec | grep status`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: SERVFAIL, id: 40999
    ```

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
* i3D
* EdgeUno
* Equinix Metal (FKA: Packet, Packet.net, or Packethost)
* Path.net (Path Network)
* E-MAX (Bratislava, SK)

These organizations are also listed on the Sponsors page of the Quad9 website: [quad9.net/about/sponsors](https://quad9.net/about/sponsors)

If you are trying to simply determine if you are using Quad9, you can visit [on.quad9.net](https://on.quad9.net) instead of relying on a DNS leak test. However, a DNS leak test can be useful to ensure you're exclusively using Quad9, which is required to ensure that all of your DNS requests will be protected by Quad9.

## Oblivious DNS over HTTPS / ODoH

Offering [Oblivious DNS over HTTPS (ODoH)](https://datatracker.ietf.org/doc/rfc9230/) is not currently on the Quad9 roadmap. Although there is [an open feature request in GitHub](https://github.com/PowerDNS/pdns/issues/10652) to support ODoH in the open-source software used by Quad9, and assuming that is implemented in the future, there are significant security concerns and complexities involved that would make this an incredibly difficult protocol to support while maintaining the integrity of our services. Quad9 will continue to keep this in mind in the future and once supported in software.

## Cache Flushing

Quad9 does not currently offer a public, cache flush tool. There are various technical and security limitations that prevent Quad9 from offering this feature at this time.

Quad9 does not honor cache flush requests submitted to our support team.

Quad9 is working with our open-source software partner to make the necessary performance and scaling improvements to the code base to be able to support this in the future.

Before making major changes in DNS, such as changing authoritative DNS services, a standard practice is to lower the TTL significantly of the modified resource records and allowing enough time to elapse for the previous TTL to expire, thus providing the opportunity to revert the changes with limited impact in case of misconfiguration.

In the future, Quad9 may be able to offer a cache flush tool or honor cache flush requests submitted to our support team, but there is no timeline for offering this feature.
