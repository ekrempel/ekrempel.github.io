---
layout: post
title: Password manager for desktop and mobile with 2nd factor
---

A long time ago I started using [KeePass](https://keepass.info/) as my password manager. Once I started working from multiple machines I had to synchronize the database between  used PCs. Later I started syncing the database to my phone to have an easy mobile access. Even later I had the wish to secure access to my database with an 2nd factor for improved security. That started a long journey to my new password managenet.

### Requirements
These are the requirements I had for my password management:
1. Open Source
2. Self hosted
2. Windows Client
3. Android Client
4. (Optional) Linux Client
4. Easy to use 2nd factor such as [YubiKey](https://www.yubico.com/)
5. High level of usability

After comparing the availible systems I wanted to continue using KeePass as my password manager. Sadly there is no FIDO U2F support for KeePass and I do not assume that this will change in the (near) future. There are multiple other ways to secure a KeePass DB wit a 2nd factor as different plugins are availible.
* [KeeChallenge](https://brush701.github.io/keechallenge/)
* [KeeOtp](https://bitbucket.org/devinmartin/keeotp/wiki/Home)
* [OtpKeyProv](https://keepass.info/plugins.html#otpkeyprov)

I did choose KeeChallenge as it has some major advantages over the other solutions. You can easily programm multiple 2nd factor devices with the same secret and thereby backup your key. Compared to Otp you do not need to worry about keeping multiple keys synchronized. Compared to OtpKeyProv you can use a "real" hardware 2nd factor and do not use your smartphone as a 2nd factor.

I chose a [YubiKey Neo](https://www.yubico.com/products/yubikey-hardware/yubikey-neo/) as my main device. I has the main advantage of offering NFC that will comme in handy later. Additionaly I own another YubiKey as a backup that is stored in a safe place. You can follow this [tutorial](http://www.kahusecurity.com/2014/securing-keepass-with-a-second-factor/) to configure your DB and a YubiKey.
