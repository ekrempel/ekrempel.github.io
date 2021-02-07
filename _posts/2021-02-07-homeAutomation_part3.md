---
layout: post
title: Eltako F4SR14-LED actuator and openHAB
---

In this blog post I will give you a short abstract how I managed to get my Eltako F4SR14-LED  actuators working with [openHAB](https://www.openhab.org/). I do not aim to write a self-sufficient how-to for you but want to show some of the things I learned during my journey. It should go without saying that I am in no way responsible if the documented method does not work for you. Good sources for further reading are the [EnOcean part of the openHAB documentation](https://www.openhab.org/addons/bindings/enocean/) and the github page of the [EnOcean Binding](https://github.com/fruggy83/openocean). Another great source for the documentation of Eltako actuators is the [wiki of FHEM](https://wiki.fhem.de/wiki/EnOcean_Starter_Guide#UTE-Teach-In).

In the last post I already mentioned that working with Eltako actuators is more complicated that using the EnOcean autodiscover feature as they do not support the UTE teach-in. So what you have to do is the following:

1. Great an new Thing according to your actuators
2. Define a teach-in button in the openHAB UI
3. Prepare your actuators for teach-in
4. Trigger a teach-in via the UI
5. Put your actuators back into default mode

This rather laborious process is not a fault of the Binding developers of openHAB but to the limitation of the Eltako actuators. The only thing the openHAB developers could do is to present you with an teach-in button while creating a Thing to streamline the process a little. Maybe this will be integrated in the future when we see more usage of the UI-based configuration. But lets get started.

###  [F4SR14-LED](ttps://www.elektroland24.de/smarthome/Eltako-Funk/Schalten-per-Funk-oxid-1/Funkaktoren-Schalten-REG/Eltako-F4SR14-LED-Funk-Schaltrelais-fuer-230V-LED-s-4-Kanaele.html)

The easiest actuator to teach-in in my setup is the F4SR14-LED. It controls up to four different lights. To work with it we start by greating the correct Thing. Go to Settings -> Things and press the "+" in the lower right corner. Here select EnOcean Binding and Switching/Dimming Actuator. 

![EnOcean UI to configure a F4SR14-LED Thing](/images/openhab_enocean_switch.png){: width="600" }

Make sure to select the EnOcean bridge you configured earlier. Unfortunately you have to provide openHAB with the EnOceanId of the device. There are at least two ways to find them. 

If you are replacing/adding to the Wibutler as I was doing, you can see the EnOceanId in the Wibutler App. This is the easy way. 
If this is not possible you will need to use the [PCT14 Software](https://www.eltako.com/de/software/gfvs-software-pct14.html) and connect to your system to find the baseId. The first actuator will have the EnOceanId = baseId + 1. Here it gets a bit messy as different actuators have a different set of channels and every channel uses a Id.

* Eltako FSB14 -> 2 Channels
* Eltako F4SR14-LED -> 4 Channels
* Eltako FUD14 -> 1 Channel

I try to give you an example so that you can find your EnOceanIds. So assume your system looks like this: F4SR14-LED, F4SR14-LED, FSB14, FUD14 and your baseId is: ffe2c000. The first F4SR14-LED has the EnOceanId ffe2c001 and uses four channels. The second F4SR14-LED has the EnOceanId ffe2c005 and uses four channels. The FSB14 has the EnOceanId ffe2c009 and uses two channels. **The second tricky part of EnOceanIds is, that they are written as Hexadecimal**. Therefore the EnOceanId of the FUD14 is ffe2c00B and not as you might assume ffe2c010.

Leave the Sender Id empty, as the Binding will select the correct Id by itself and create the Thing. 

After creating the Thing we will have to teach it to the actuator. Go to Settings -> Thing and select the newly created Thing. Switch to the Tab Channels and activate Show advanced. Here you will find the Channel "Teach In". 
![EnOcean UI to configure a F4SR14-LED Thing](/images/openhab_enocean_teachin.png){: width="600" }

Select it and press "Add Link to Item...". In this dialogue select "Create a new Item" and press "Link". 

![EnOcean UI to create a teach-in button](/images/openhab_enocean_teachin2.png){: width="600" }

### Before we start with teach-in
There are three important things you should be doing before going any further.

1. Make photos of all you actuators
2. Use the PCT14 software to make a backup of your EnOcean settings
3. Make sure that nobody will accidentally press any of your EnOcean switches when you activated teach-in

Now we created the Thing and prepared a software button to trigger the teach-in event. Next we will have to prepare the F4SR14-LED actuator to teach him a switch. You can find more information in the [official documentation](https://www.eltako.com/fileadmin/downloads/de/_bedienung/F4SR14-LED_30014076-1_dt.pdf). Use a small screwdriver to put you F4SR14-LED in the teach-in mode. Set the lower selector to the channel you want to configure. After that set the middle selector to "LRA". The LED of the actuator will blink rapidly. While it is blinking press the teach-in button we defined in the last step. The blinking of the actuator will stop and teach-in is finished. (Sometimes you have to press the teach-in button a second time until it is accepted, don't be alarmed.)

![Set the F4SR14-LED into teach-in](/images/F4SR14-LED.png){: width="200" }

**Please note that the actuator will not accept any switches until you put it back into default!** Please remember to put the lower selector back to "AUTO" and the middle selector to "AUTO 1".

You now should have created you first Thing and can test it. Go to Settings -> Things and select your newly created switch. Select the Tab Channels and select the Channel "Switch". Select it and press "Add Link to Item...". In this dialogue select "Create a new Item" and press "Link". You should now be able to use this switch to control you lights.
