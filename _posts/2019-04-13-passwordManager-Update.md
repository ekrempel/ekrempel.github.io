---
layout: post
title: YubiKey 5 with USB-C as 2nd factor on mobile
---

As the NFC of my YubiKey Neo seems to have deteriorated over time, I now updated my setup. I bought a new [YubiKey 5C](https://www.yubico.com/product/yubikey-5c/) with a USB-C connector. With it you can connect a YubiKey to a compatible Android Phone and use it as 2nd factor.

The update was painless and took me only 10 minutes. I first configured my YubiKey 5C the same way I had configured my YubiKey Neo (Challenge Response; HMAC-SHA1 with a fixed 64 byte secret). 

This is all I had to do to use the new YubiKey 5C on my desktop. 

To use the Stick on my Android phone I had to change the Challenge/Response App I was using. I replaced YubiChallenge with [ykDroid](https://play.google.com/store/apps/details?id=net.pp3345.ykdroid) that offers Challenge/Response via NFC and additionally via USB-C. Make sure to uninstall YubiChallenge to make sure that ykDroid is used. After that all you have to do is plug in your YubiKey and you can use it as 2nd factors to unlock your database.

