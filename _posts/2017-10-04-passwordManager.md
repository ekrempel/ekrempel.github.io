---
layout: post
title: Password manager for desktop and mobile with 2nd factor
---

A long time ago I started using [KeePass](https://keepass.info/) as my password manager. Once I started working from multiple machines I had to synchronize the database between  used PCs. Later I started syncing the database to my phone to have an easy mobile access. Even later I had the wish to secure access to my database with an 2nd factor for improved security. That started a long journey to my new password management.

### Requirements
These are the requirements I had for my password management:
1. Open Source
2. Self hosted
2. Windows Client
3. Android Client
4. (Optional) Linux Client
4. Easy to use 2nd factor such as [YubiKey](https://www.yubico.com/)
5. High level of usability

### Setting up the DB and the Desktop
After comparing the availible systems I wanted to continue using KeePass as my password manager. Sadly there is no FIDO U2F support for KeePass and I do not assume that this will change in the (near) future. There are multiple other ways to secure a KeePass DB wit a 2nd factor as different plugins are availible.
* [KeeChallenge](https://brush701.github.io/keechallenge/)
* [KeeOtp](https://bitbucket.org/devinmartin/keeotp/wiki/Home)
* [OtpKeyProv](https://keepass.info/plugins.html#otpkeyprov)

I did choose KeeChallenge as it has some major advantages over the other solutions. You can easily program multiple 2nd factor devices with the same secret and thereby backup your key in a secure manner. Compared to Otp you do not need to worry about keeping multiple keys synchronized. Compared to OtpKeyProv you can use a "real" hardware 2nd factor and do not use your smart phone as a 2nd factor.

I chose a [YubiKey Neo](https://www.yubico.com/products/yubikey-hardware/yubikey-neo/) as my main device. I has the main advantage of offering NFC that will come in handy later. Additionally I own another YubiKey as a backup that is stored in a safe place. You can follow this [tutorial](http://www.kahusecurity.com/2014/securing-keepass-with-a-second-factor/) to configure your DB and a YubiKey.

### Syncing the DB
As we have a high level of trust in the encryption used by KeePass we can use any available cloud such as Dropbox or Owncloud to synchronize our DB.

### Accessing the DB on mobile
After finishing the setup on your desktop it is time to configure your system on Android. First you will have to install multiple apps.

* [KeePass2Android](https://play.google.com/store/apps/details?id=keepass2android.keepass2android&hl=en)
* [YubiChallenge](https://play.google.com/store/apps/details?id=com.yubichallenge&hl=en)

The section **Yubikey Challenge/Response with Android** of this [turorial](https://b3n.org/yubikey-two-factor-authentication/) will give you a step by step guide how the configure both apps. KeePass2Android is used to manage your passwords and YubiChallenge will be used for the communication with KeePass2Android. The work flow will be as follows:

To open your DB KeePass2Android will be required to solve the challenge combined with the database. It will send the challenge via an [Intent](https://developer.android.com/reference/android/content/Intent.html) to YubiChallenge. This will ask you to swipe your YubiKey Neo to your device. Via NFC your smart phone will send the challenge to the Neo which will solve it. The result is delivered via NFC to YubiChallenge which will deliver the result of the Intent to KeePass2Android.

### Conclusion
By using a 2nd factor we can greatly improve the security of our KeePass database. The usability is far from perfect and I assume not many people will want to search their Yubikey every time they want to access their database. For me this solution brings me the wanted level of security to trust my database to a mobile device.
