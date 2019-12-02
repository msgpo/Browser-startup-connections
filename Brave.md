## Overview

Brave is one of the good Chromium based forks which is well maintained, [well documented](https://github.com/brave/brave-browser/wiki) and includes all patches from [ungoogled-chromium](https://github.com/Eloston/ungoogled-chromium/issues/543). The Browser gets [audited regularly](https://github.com/brave/brave-browser/wiki/Security-Audit-Guide), from the community and after a final release from a independent team.

Brave is special because it includes Tor (_no other Chromium based browser does that_), only Firefox (ESR) a.k.a. Tor Browser Bundle includes "Tor".

Brave often gets criticized for it's optional "crypto" implementation (BAT). This is an optional feature and can be enabled and disabled based on your own needs, the goal is to find an alternative to traditional ads and help content creates but maintaining the own privacy. Brave DOES NOT "mine" in the background, this is a false spread myth. [All is well documented](https://brave.com/de/brave-rewards/).

While Brave want to block trackers (same like Firefox does since FF 72), brave offers a solution to the "ads" problem. No other browser provides other alternatives.


## Services & Features which are disabled in Brave

Brave disables and removes [a lot](https://github.com/brave/brave-browser/wiki/Deviations-from-Chromium-(features-we-disable-or-remove).


## Services & Features which are been [proxied](https://github.com/brave/brave-browser/wiki/Proxy-redirected-URLs)

* SafeBrowsing requests
* Geolocation requests
* Plugin updates
* Certificate revocation requests
* Page translation (replaced with Microsoft cognitive services (currently disabled by `ENABLE_BRAVE_TRANSLATE_GO` build flag))
* Requests for CRLSets
* Requests for component updates
* Requests for spellcheck dictionaries

The full list can be found over [here](https://github.com/brave/brave-browser/wiki/Proxy-redirected-URLs), in other words Brave uses it's own "black hole" to proxy all outgoing connections.



## Calls during startup

* The first call is been made for the integrated _Tor client_, this is basically a connectivity check which is mandatory, otherwise Brave will fallback to other connection methods.
* The second connection is done by the implemented "content-blocking" method.
* The third call is to connect to `brave-core-ext.s3.brave.com`, this is documented and it point to the integrated HTTPS Everywhere integration. It also points to local tracking protection files.
* `static.brave.com`, is connected for "Safe Browsing" updates.
* `go-updater.brave.com` is been connected (_as the name already suggest_) for updates (extensions, plugins). The request "spam" you possible see is okay and nothing to worry about.
* `brave-core-ext.s3.brave.com` forwards the update events, this contains some information like update channel, OS information as well as how many memory is available. Depending on how the server response to the input he gets, it will (or will not) update extensions.

Brave typically does 23 requests during the first startup. Further startups made more/less connections (depending on the settings/if there is an update etc.).


## Conclusion

Brave does a good job, the connections are proxied, secured and all is been controlled. Depending on what functions you set within the settings you will automatically see more or less connections, keep in mind we use default settings (out-of-the-box), you can disable Safe Browsing and there will be no startup connection.


