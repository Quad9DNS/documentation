## Overview

Pi-Hole is a popular DNS forwarder, often used primarily for blocking domains specifically associated with ads and tracking.

## Pi-Hole Setup

For detailed setup instructions of Pi-Hole itself, please see the [Official Pi-Hole Documentation](https://docs.pi-hole.net/).

## Quad9 Setup

Once you have installed Pi-Hole and can access the administration panel, Quad9 is already one of the default options.

* In the Admin panel, navigate to `Settings` -> `DNS`
    * Check both IPv4 boxes next to Quad9 (filtered, DNSSEC)
        * If your network support IPv6, it's also recommended to check both IPv6 boxes. If you're not sure if IPv6 is configured on your network, you can test that here: https://test-ipv6.com/

* Check/Enable the options:
    * `Never forward non-FQDNs` and `Never forward reverse lookups for private IP ranges` to prevent sending unanswerable DNS queries to Quad9.
        * Click `Save` at the bottom.

### Verify Configuration

Once Quad9 has been configured in Pi-Hole, you can configure your router or a single computer to use the Pi-Hole's IP address as a DNS server. If the Query Log is enabled (Settings -> Privacy [tab]), you should see Quad9 recorded in the Status column:

You can also confirm if Quad9 is being used manually on Linux, MacOS, or Windows.

### Blocked Domains

Domains which are blocked by Quad9 will record Blocked (external, NXRA) in the Status column of the Query Log:

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
