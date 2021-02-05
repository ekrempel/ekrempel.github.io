---
layout: post
title: Home automation (Part 1)
---

So I started working on home automation. If you know me you will find this funny as I always wanted to stay clear of it. Not because I don't see the value, but because I assume that it is a huge time sink. Most components are not mature enough to allow me to built a system once an just use it in the future. So you will have to research, update, adapt and replace components all the time. Basically the only valid option is to make it a hobby so that it does not feel like a chore. To be fair, I am not quite sure if home automation is a hobby of mine, but I don't mind most of the time I have invested so far.

But why did I actually start with home automation? Our home came equipped with a [Wibutler](https://www2.wibutler.com/). I would describe it as an universal smart home bridge. I looks nice, combines [WLAN](https://en.wikipedia.org/wiki/Wireless_LAN), [Z-Wave](https://en.wikipedia.org/wiki/Z-Wave), [ZigBee](https://en.wikipedia.org/wiki/Zigbee) and [EnOcean](https://en.wikipedia.org/wiki/EnOcean) into a single device and makes it easy to integrate a broad variety of systems <https://shop.wibutler.com/>. While the hardware is great I don't understand many of the design choices of the App.

Of course you can interact with every connected device individually like switching a light or opening blinds. Additionally you can define if-then-rules: "if the front door is opened activate the lights at the entrance" and time-based-rules: "lower this blind at that time". You can even define four profiles "at home-day", "at home-night", "away" and "holiday". This can be used to define a system that moves your blinds during your holiday. So with all this functionality why am unhappy with the software?

1. The interaction with the App is cumbersome. If I want to switch a light I have to unlock my phone, start the App, wait around 5 seconds until the App has synced with the Wibutler, search the correct light in the App and then switch it. All I want to have is a widget that allows me to define a button that triggers an event. I assume it would take the developers a max of 1 day to include this (considering implementation, testing and documentation), but the feature request is open since June 2019. <https://community.wibutler.com/topic/958/virtuelle-taster-als-android-widget>

2. I want to have groups of devices do the same thing. For example I want the two blinds in the living room to go up/down at the same time or have both lights in living room to dim to the same value. Today I have to select them individually in the App and select the action. Here I would want to define groups or at least define my own button that triggers an event. The oldest feature request for groups I could find was back to 2016 <https://community.wibutler.com/topic/1245/ip-basierte-dienste-und-ger%C3%A4te>.

3. Even when smart phone and Wibutler are in the same network all traffic is routed via the Cloud back end. 

3. So far the system is App (iPhone or Android) only. There is no browser based interface.

4. There is no public API that allows me to interact with the system. I don't except to have access to the whole system but would like to send simple commands via an API. While this would not be an super easy task to do it would allow me to use the Wibuter as a really universal smart home bridge. Unfortunately the feature request is open since 2016. <https://community.wibutler.com/topic/364/json-api>

5. While I am fine with waiting for new features there is no public roadmap what is planed and when to expect it. Most feature request in forum are open since a really long time and I feel that the speed of (the front end) development is slow.

So while I really like the hardware and the idea of having a company responsible to work on updates and the integration of new features I don't feel that Wibutler works for me. Therefore I will start looking into open source smart home solutions and try to find my setup.