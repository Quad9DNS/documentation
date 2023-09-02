## What is EDNS Client Subnet (ECS)?

Quad9's `9.9.9.11` service supports ECS.

EDNS Client Subnet (ECS) allows Quad9 to send a portion of your IP address to authoritative name servers, which helps major content providers (CDNs), such as Google, Microsoft, etc, accurately determine your geolocation.

ECS will have no effect on which Quad9 location your queries are sent to, it simply effects what information Quad9 forwards to the authoritative name server and may effect what IP address they return back. Quad9 uses anycast addressing to ensure you are routed to the nearest Quad9 location available to you regardless of whether or not you use our ECS service.

Since ECS does not play any role in determining where your queries are sent to, it does not have any positive or negative effect on the round trip time (ping) to Quad9

ECS can be viewed as a trade off between privacy and getting geospecific content. One option for the privacy focused user is to leave it disabled and only enable it if you notice a specific domain not delivering you the correct content or not loading at all.
