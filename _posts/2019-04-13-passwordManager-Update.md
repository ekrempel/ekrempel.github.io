---
layout: post
title: YubiKey 5 with USB C as 2nd factor on mobile
---

As the NFC of my YubiKey Neo seems to have deteriorated over time I now updated my setup. I bought a new [YubiKey 5 C](https://www.yubico.com/product/yubikey-5c/) with a USB C connector. With USB C you can connect a YubiKey to a compatible Android Phone and use it as 2nd factor.

The update was easy and took me only 10 minuets. I first configured my YubiKey 5 C the same way I configured my older YubiKey Neo (Challenge Response; HMAC-SHA1 with a fixed 64 byte secret). 

This is all I had to do to use the new YubiKey 5 C on my desktop. 

To use the Stick on my Android phone I had to change the Challenge/Response App I was using. I replaced YubiChallenge with [ykDroid] (https://play.google.com/store/apps/details?id=net.pp3345.ykdroid) that offers Challenge/Response via NFC and additionally with USB C. Make sure to uninstall YubiChallenge to make sure that ykDroid is used. After that all you have to do is plug in your YubiKey and you can use it as 2nd factors to unlock your database.

