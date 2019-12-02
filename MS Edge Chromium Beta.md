## Overview

MS Edge (Chromium) is still (at the time of writing) in beta stage, a lot of things can be changed and we should consider to check the Browser [when it's in a final form](https://www.theverge.com/2019/11/4/20942038/microsoft-edge-chromium-release-date-new-logo-features).

MS Edge Chromium is [better documented as Chrome](https://docs.microsoft.com/en-us/deployedge/microsoft-edge-policies) even in his unfinished form. The community basically does the entire work here.


## Services & Features which are disabled in Chrome

Similar like Brave, [MS Edge Chromium removes several functions](https://twitter.com/h0x0d/status/1115310035825872896).

* Safe browsing
* Nearby messages
* Link Doctor
* Ad blocking
* User data sync
* Spellcheck
* Suggest
* Translate
* SmartLock
* Form Fill
* Push Notifications
* Web Store
* Extension Store
* Maps Geolocation
* Google Now
* Speech input
* Google Pay
* Drive API
* Chrome OS hardware id
* Device registration
* Google Maps Time zone
* Google Cloud Storage
* Cloud Print
* Google DNS
* Supervised Profiles
* Address Format
* Network Location
* Network Time
* Favicon service
* Google Cloud Messaging
* Single sign-on (Gaia)
* Content Hash Fetcher
* Flighting Service
* Component Updater Service
* RAPPORT service
* Chrome OS monitor calibration
* Chrome OS device management
* Android app password sync
* Offline Page Service
* Feedback
* Domain Reliability Monitoring
* Data Reduction Proxy
* Chrome Cleanup
* Developer Tools Remote Debugging
* iOS Promotion Service
* One Google Bar Download
* Brand Code Configuration Fetcher
* WebRTC Logging
* Captive Portal Service

The list was fist provided by [@h0x0d](https://twitter.com/h0x0d/status/1115297361763287040) and [@gus33000](https://twitter.com/gus33000/status/1115506593582469120).


In other words, MS Edge Chromium follows Brave's and original Chromium footsteps and disables or removes the controversial components. However the list is misleading because not Chromium features are been disabled, it's the opposite Chrome based features are been disabled. It’s more of a list which invasive parts were replaced by Microsoft equivalents.

MS Official writes that the development focus is on

* Accessibility
* Editing
* Security
* ARM64
* Fonts
* Tooling
* Authentication
* Layout
* Touch
* Battery life
* Scrolling
* Web Standards


## Services & Features which are been proxied

* None. It follows the same rules as Chromium.


## Calls during startup

Chrome is (as for now) the browser with the most startup connections. I saw over 134 connections, MS Edge Chromium deeply integrates into MS Windows 10, that been said the startup connections are depending if or if you're not use a MS Account under Windows. If you choose to use an MS Account in Windows 10, MS Edge Chromium tries to connect to that account and logs you automatically in. This is really dangerous and might expose some information, especially if you're not alone on the PC.



* `speech.platform.bing.com` is been called to obtain the `trustedclienttoken`. The token holds the information about the current device. It's unclear what information are exactly been transmitted since everything is encrypted.
* The second request goes to `clients2.google.com`, in this case it uses Chrome Media Router function to call get XML.
* The third connection goes to `ntp.msn.com`, NTP in this case means New Tab page. The information is typically 62KB long. The information contains information regarding the status page among with some local data, it's unclear why this is been send out.
* `go.microsoft.com` is been called with the information for the local header. It basically points to the `/welcome` windows insider page. Whenever a MS domain is been connected smart screen will automatically checks the connection.
* `windows.com` uses Windows own [Activity History](https://support.microsoft.com/en-us/help/4468227/windows-10-activity-history-and-your-privacy-microsoft-privacy) which is by default enabled.
* `clients2.google.com` which points to `redirector.gvt1.com` is the same like on Chrome, it basically downloads the extension CRX from Google's cryptic redirector. The URLS are always loaded unencrypted over HTTP to perform a basic hash comparison.
* `akamaized.net` is been [used for NTP](https://ntp.msn.com/compass/antp?locale=en-US&dsp=1&sp=Bing&fre=1&startpage=1).
* `activity.windows.com` is more than once been called. It periodically checks for your eMail address and for Windows 10 login information.
* `microsoftedgeinsider.com` is been used to load the second "welcome" tab. The page is online served, contains CSS, Fonts etc and triggers more connection.
* `ntp.msn.com` is been used not only as new tab page, it also triggers `scorecardresearch.com`, the information it collects is "HTTP 204 No Content.".
* The `microsoftedgeinsider.com` website calls out to `platform.nitter.net` which redirects to `static.ads-nitter.net`. Once the request is made, Google Tag Manager kicks in and forwards the "hello" message to `mem.gfx.ms` (which is to track specific events). This is very critical because of user tracking and it calls other service like reddit, Google, Facebook and others which are typically been used for "social buttons". MS can simply implement "data friendly" like buttons to avoid this, however, this is a website problem and not really related to the startup connection problematic since the Browser just forwards the events. The best would be if MS drops the second tab and let it go. MS officially said they are working on a way to reduce the third-party calls on their insider website.
* `dc.services.visualstudio.com` collects user ID, DOM processing time and more information, the intent is coming from the Chrome Media Router feature.


MS Edge downloaded 14,8 MB of data (in total).

## NO conclusion

MS Edge Chromium as well as the "insider" page is beta, lots of things can change over time and MS already did changed a lot since I wrote this in July 2019.

There is no final conclusion, I do not like to review beta products in general because there are maybe known bugs, problems etc which are often already addressed in the final product.
