## Overview

Mozilla Firefox is one of the best alternative to Chrome/Chromium based browsers. Mozilla claims to "secure the web" and Firefox should help to reach that goal.

Firefox is very popular in the privacy community and is been trusted by millions of people. Same like Chrome, Firefox isn't perfect and had his own "privacy incidents" during the years.


## Services & Features which are disabled in Chrome

* Firefox disables specific privacy "unfriendly" or security critical Web API's by default, others can be optionally disabled via about:config.


## Services & Features which are been proxied

* None.


## Calls during startup

This [article is outdated](https://kb.mozillazine.org/Connections_established_on_startup_-_Firefox), some things are still valid while others are not anymore correct.

Firefox (not the Tor or ESR or "special" EME free version) calls 26 domains (incl. telemetry, blocklist, googletagmanager, snippets, open264 etc).


* The first connection is typically `detectportal.firefox.com`, which is not done via HTTPS 443, it's over HTTP. This is okay, because the service is made to detect public networks.
* `ocsp.digicert.com` is been used for Online Certificate Status Protocol (OCSP) , which is basically spoken a check for revocation of bad certificates. The Browser does not checks the OS certificates but it checks his store twice once during the startup sequence and another time during the tab opening process (_for the "hello welcome tab which you see right after you start the browser_).
* `snippets.cdn.mozilla.net` includes 12KB bits of information, it's packed in a .JSOn file. If you open the file you see it checks the OS version (x86/x64).
* `tiles.services.mozilla.com`, is a part of tiles which includes [activity stream](https://github.com/mozilla/gecko/blob/central/testing/profiles/common/user.js#L9-L10). The information submitted here are non critical, you see another .JSOn file stores the information, such as `cfr-fxa` among other information of CFR, that's really cool.
* `tiles.services.moz` itself contains some basic information, like locale,, profile creation date, release channel, version, region (typically set to "UNSET" because you can download FF in your own language and then it sets the string based on your location). `event=AS_ENABLED` basically says that the activity stream service is running.
* `mozilla.org` calls other stuff like Google Tag Manager and Google Analytics, Basically no news because Mozilla and Google still having a deal together.
* `normandy.cdn.mozilla.net` is been explained by Mozilla, the description is a bit cryptic: ["... is a feature that allows Mozilla to change the default value of a preference for a targeted set of users, without deploying an update to FF."](https://wiki.mozilla.org/Firefox/Normandy/PreferenceRollout) What it contains is some basic information, like revision, extension, if the addon is signed or not, among the information if there is an approval request made or not. The server typically returns for example: `{"country":"US","request_time":"2019-07-05T16:02:21.162561Z"}`
* [Safe Browsing](https://wiki.mozilla.org/Security/Safe_Browsing) differs from brave and is overall better handled in brave, since it's been proxied and Google is never directly called. However, Mozilla Firefox downloads the list [from Google directly but explains it very well](https://support.mozilla.org/en-US/kb/how-does-phishing-and-malware-protection-work). [The "Feeding the Cloud" blog basically explains how it works](https://feeding.cloud.geek.nz/posts/how-safe-browsing-works-in-firefox/) in-depth.
* `firefox.settings.services.mozilla.com` is been called by the _normandy.cdn_ it is been called from snippets.
* Certificates or the information are downloaded from `content-signature-2.cdn.mozilla.net`.
* Update checks are made periodically, even after the first startup. We assume that we installed the latest Firefox version, which means the XML response will be empty . The `<updates>` object is not empty if there is an update.
* More normandy checks are done, for features like LockWise ("Have I been Pwned") etc. This is on purpose.
* Every `aus5` based calls are sub-spooled from `gvt1.com`, the original attempt is coming from WideVine (openh264 plugin).
* `incoming.telemetry.mozilla.org` typically submits 37,097 bytes of information during the first start.


Firefox downloaded 16,2 MB of data (in total)


### Facts
* Mozilla Firefox uses telemetry, it's documented and you man manually opt-out, not cool but possible.
* Mozilla has the most startup connections with MS Edge and Chromium. Only Brave has the best out-of-the-box experience.
* Mozilla does offer, like no other Browser, a EME free build, this is the correct way, because no user should be forced to mess with about:config or about:flags (_not for a privacy oriented browser_). Mozilla should take my advice more serious and work with the community closer together to get rid of all "about:config hardening" projects, this is simply not the correct way to "securing the web". The community want to do something, but Mozilla does not care (enough). Tor simply has the (privacy and security wise) better migration and better out-of-the-box experience. Migrating and porting features from Tor into Firefox is complicated, causes lots of problems and is often not worth it because the "privacy gain" you get is questionable can be reached by using a VPN.
* Reducing the startup connections via flags/config is on all browsers possible but none of the browser can eliminate all of the startup connections.



## Conclusion

Firefox has together with MS Edge Chromium the most startup connection. Unless MS Edge Chromium Mozilla by default opt-out of telemetry while MS Edge Chromium opt-in by default (which is the better way). It's unclear why Mozilla do not take my advise serious which I made in FF 4.x I send a 20 page proposal to Mozilla with ideas and improvements back in the day, which got ignored, the bugzilla entries are full of other good ideas as well as feature request which often taking years until they get attention (Chrome and MS Edge is not better here).

Firefox is not as good (when it comes to startup connections) as most people think. Mozilla did not invented the wheel new nor did they made efforts to reduce the connections, comparing to the old article written in 2013 more startup connections are added for questionable privacy "features".
