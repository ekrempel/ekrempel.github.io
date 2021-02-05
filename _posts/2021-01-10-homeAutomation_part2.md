---
layout: post
title: Home automation first steps with openHAB (Part 2)
---

After accepting that the Wibutler will not be able to meet my requirements I started looking into different solutions. I had two main requirements. The new system must be able to control my existing [EnOcean](https://de.wikipedia.org/wiki/Enocean) devices and should have an active community so that the solution will be around for a long time. Additionally I looked for systems that are able to connect to a broad variety of components. 

First, I started looking into [Home Assistant](https://www.home-assistant.io/). I had used it in the past for a small project and had some experience. Unfortunately Home Assistant is only able to read EnOcean but cannot control it. If you want to control an EnOcean system you have to use configure [FHEM](https://fhem.de/) to control your EnOcean and link it to Home Assistant via MQTT. While it seems to work there were to many moving parts for my liking.  

Of course it would be another solution to just use FHEM for all home automation. While FHEM seems extremely powerful I did not like the way you interact and configure the systems and are not a fan of the existing GUIs. So after playing some days with FHEM I decided against it.

After some more research and testing I settled with [OpenHab](https://www.openhab.org/) for my system. As there was a major new release with openHAB 3.0 in December 2020, there is a lot of documentation not yet matching the system. Therefore I decided to document my way to built my home automation system to help other people with the same journey.

My first goal was to be able to control the following devices:
* [Eltako FSB14](https://www.elektroland24.de/smarthome/Eltako-Funk/Rollladen-per-Funk/Funkaktoren-Rollladen/Eltako-FSB14-Schaltaktor-Rollladen-mit-2-Kanaelen.html) (Controls up to two rollershutters)
* [Eltako F4SR14-LED](https://www.elektroland24.de/smarthome/Eltako-Funk/Schalten-per-Funk-oxid-1/Funkaktoren-Schalten-REG/Eltako-F4SR14-LED-Funk-Schaltrelais-fuer-230V-LED-s-4-Kanaele.html) (Controls up to four lights)
* [Eltako FUD14](https://www.elektroland24.de/smarthome/Eltako-Funk/Dimmen-per-Funk/Funkaktoren-Dimmen-REG/Eltako-FUD14-Universal-Dimmschalter-LED-ESL-bis-400W.html?listtype=search&searchparam=fud14&&order=&&order=#FUD14) (Dimmer for one light)

To interact with Enocean devices you need a gateway. The most common type is the [USB 300](https://www.enocean.com/de/produkte/enocean_module/usb-300/) that works well with a Raspberry Pi. 

### Basic installation and testing

Installation of openHAB on a Raspberry Pi is easy and well documented. I used the Raspberry Pi prepackaged SD card image as described here: <https://www.openhab.org/docs/installation/openhabian.html#raspberry-pi-prepackaged-sd-card-image>. I decided to work with the UI-driven configuration of openHAB. While many tutorials you find use the file-based configuration I found some sources that most development goes to UI-driven systems in the future. 

After installation you should play around with openHAB and check out the [Tutorial](https://www.openhab.org/docs/tutorial/). Once you are a little bit familiar with the system and understand the difference between a Thing and a Item it is time to work on the EnOcean actors. 

The first step is to install the [EnOcean Binding](https://www.openhab.org/addons/bindings/enocean/) into your openHAB. After that add the USB 300 gateway as a Thing. In my case it was automatically detected once I plugged it into the Raspberry and rebooted it. I just had to click on the Inbox and accept the detected parameters. To test your installation you can try to read EnOcean communication. To do this go the Things, klick the "+" in the lower right corner and select the EnOcean Binding. In the new screen you should see your see your gateway listed and click on the button "Scan". While the scan is running press any of you EnOcean wall switches. The should be register a new Thing. You can see an example in the screenshot below.

![EnOcean Autodiscover detecting wall switches](/images/openhab_enocean_discover.png){: width="600" }

Unfortunately this technique does not work for actors like the FUD14 FSB14 or F4SR14-LED. They need a more complicated teach-in technique that I will describe in the next post.
