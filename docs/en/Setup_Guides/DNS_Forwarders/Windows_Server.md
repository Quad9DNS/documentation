## Overview

Set up Quad9 in Windows DNS Server for use in DNS forwarding.

!!! note
    Before proceeding, please refer to our [DNS Forwarder Best Practices](https://docs.quad9.net/Quad9_For_Organizations/DNS_Forwarder_Best_Practices/) article.

## Instructions

* Open `Server Manager` from the `Start` menu.
    * From `Server Manager`, select `Tools` > `DNS`

* From the DNS Manager, right-click your server and select `Properties`
    * Select the `Forwarders` tab and then select `Edit`.
        * Add the following IP addresses: `9.9.9.9`, `149.112.112.112`
        * If your network supports IPv6, also add: `2620:fe:fe`, 2620:fe::9
            * Click "Apply"

Questions? Issues? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
