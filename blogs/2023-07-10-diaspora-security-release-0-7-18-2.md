---
title: "diaspora* security release 0.7.18.2"
url: "https://blog.diasporafoundation.org/76-diaspora-security-release-0-7-18-2"
date: "2023-07-10"
author: "Diaspora* Foundation"
feed_url: "https://blog.diasporafoundation.org/feed"
---
We just released a new diaspora* version, which addresses possible security issues when processing images uploaded by users that is affecting some system configurations. This fix was heavily inspired by Mastodon's fix for GHSA-9928-3cp5-93fm , and while diaspora*s attack surface is significantly smaller and some operating systems do ship a restrictive ImageMagick policy, this release makes sure that everyone is safe. Thank you Cure53 for finding this issue, thank you Mozilla for paying Cure53 to look into it, and thanks for Mastodon for fixing it.
