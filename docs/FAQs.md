## What is EDNS Client Subnet (ECS)?

Quad9's `9.9.9.11` service supports ECS.

EDNS Client Subnet (ECS) allows Quad9 to send a portion of your IP address to authoritative name servers, which helps major content providers (CDNs), such as Google, Microsoft, etc, accurately determine your geolocation.

ECS will have no effect on which Quad9 location your queries are sent to, it simply effects what information Quad9 forwards to the authoritative name server and may effect what IP address they return back. Quad9 uses anycast addressing to ensure you are routed to the nearest Quad9 location available to you regardless of whether or not you use our ECS service.

Since ECS does not play any role in determining where your queries are sent to, it does not have any positive or negative effect on the round trip time (ping) to Quad9

ECS can be viewed as a trade off between privacy and getting geospecific content. One option for the privacy focused user is to leave it disabled and only enable it if you notice a specific domain not delivering you the correct content or not loading at all.

## Network Providers / DNS Leak Tests

Quad9 utilizes multiple network providers in our global network. When running a DNS leak test, or determining the IP address which is used to perform the recursive DNS query using a test like:

```
dig +short A whoami.akamai.net
```

it's expected to see IP addresses owned by the following providers:

* WoodyNet (AKA PCH.net)
* PCH.net
* GSL Networks
* i3D
* EdgeUno
* Equinix Metal (FKA: Packet, Packet.net, or Packethost)
* Path Networks

These organizations are also listed on the Sponsors page of the Quad9 website: [quad9.net/about/sponsors](https://quad9.net/about/sponsors)

If you are trying to simply determine if you are using Quad9, you can visit [on.quad9.net](https://on.quad9.net) instead of relying on a DNS leak test. However, a DNS leak test can be useful to ensure you're exclusively using Quad9, which is required to ensure that all of your DNS requests will be protected by Quad9.
