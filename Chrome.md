## Overview

Google Chrome is one of the most downloaded Browser in the world, it's poorly documented and not all parts are been open source (some closed source source parts where removed in the past due toprivacy concerns).

Chrome often gets criticized from people which are not been involved into web development, browser development itself.


## Services & Features which are disabled in Chrome

* Google removed several critical API's as well as some controversial UID checks


## Services & Features which are been proxied

* None. The sandbox server isolation feature will force Chrome to use it's own "tunnel". This is optional and must be enabled via about:flags.


## Calls during startup

* The first call Chrome makes is to the googleapis domain, the information which is been transmitted here is (same like Brave and Chromium) the OS type, memory, release channel and versions tag, the response from the server is always 32 KB which including those peaces of information.
* The next call is done to contact Google accounts server, this is also to check if you have an account setup not. This is not a bug, Chrome simply does not include a "first startup" check to know if you use it the first time or now, which means it always tries to check if there is a login or not, this is on purpose and not suspicion, the call goes directly to `accounts.google.com`. The header is always 42KB big and includes ["gaia.l.a.r",[]] which indicates that no account have been found. GAIA stands for Google Accounts and ID Administration.
* `clients2.google.com` is the next connection which includes XML data, this automatically triggers `gstatic.com` which is been used for translation updates, language checks and some information regarding the extensions and app IDs.
* There are (depending on the platform) 9 extensions downloaded during the first-run, the Android version downloads less. Those CRX files are for Google Drive, Docs, YouTube GMail, Chrome Cast and the Payment server. You see those apps appearing on the "apps" page. In the near future Google will change this and only place the icon on the apps page, the apps are then only been download (and not prefetched) whenever a user really clicks on them.
* The `redirector.gvt1.com` request is for Chrome Cast, this is also used in "streaming apps" like Spotify and other partners. Redirector.gvt1.com acts as redirector without any bits of information, what will include the information for the status is r5---xs-9xep1vo-8uae.gvt1.com (_random_).
* `Docs.google.com` as well as other app based connections pointing to `accounts.google.com`, this is for the service endpoint.
* `clients2.google.com` tells the information if the extension actually really needs an update or not. It also includes the bits of information from which place the extension was installed, this is done via `installedby=other`.


## Conclusion

Whenever you type something into the search bar, it will (_of course_) submit information, however this is by design (Omnibox & search suggestions). This is nothing to worry about, it's simply how it was designed.

In my test Chrome downloaded (incl. app updates) around 7,32MB on information during the first startup. No other Browser does that, however no other browser downloads and install some Chrome apps into the browser.
