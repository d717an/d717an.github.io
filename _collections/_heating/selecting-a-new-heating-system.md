---
layout: post
title: "Selecting a New Heating System"
description: >-
  How can we update the heating system of our new-to-us home to give it some more connected features?
date: 2025-01-26
order: 10
toc: true
---

_This is the first post in a series of blogs about upgrading our underfloor heating system_

## The Status Quo

### The Danfoss System

To be clear, our home is only about ten years old, and the current heating system is not "bad" by any means. The Danfoss system consists of an efficient on-demand CV (i.e. boiler) supplying hot water for seven underfloor heating zones and one radiator in the main bathroom. Each of the Normally Open (NO) underfloor heating zones are controlled by a 24V valve actuator. The valve actuators are controlled by a [central control unit](https://store.danfoss.com/is/en/Climate-Solutions-for-heating/Hydronic-floor-heating/Service-kits-for-hydronic-floor-heating/Floor-Heating-Controls%2C-Master-Controller-CF2%2B%2C-230-0-V%2C-Number-of-channels%3A-5/p/088U0245) which can modulate how much each valve is open to control the flow rate of each heating loop. There's no pump for the heating loops - I assume our water pressure is all that drives the loop. The control unit also has a relay it uses to turn the CV on and off (using a 24V signal provided by the CV). Finally, there are three wireless thermostats in the house that use the 868Mhz frequency to communicate with the control unit.

[{% picture jpt-webp /files/heating/DanfossDiagram.png --alt DanfossDiagram %}](/files/heating/DanfossDiagram.png)

### Issues

There are only a few issues with the Danfoss system.

The first is that pairing the thermostats directly with the system is not an easy process. The previous owner of our home spent quite a lot of time trying to figure it out, and had to write detailed instructions down so that he could repeat the process if needed. Thankfully, we've been very careful to keep our thermostat batteries refreshed to avoid any losing their settings.

That brings us to the second problem. The main controller has a safety feature where if it loses contact with a thermostat for a long period of time, it will enter a "frost protection mode", and periodically turn on the heating for the zone without a thermostat signal. It sounds useful, but we heard unfortunate stories from neighbors who would return home and find their home a nice and toasty 25C+, not great with sky-high energy prices.

Third, the main bathroom radiator is controlled by a simple TRV that has no way to call for heat from the CV - it will only get heat if you've turned on the heat in another room.

Finally, I would really like to have modern connectivity for our heating system. I'd love to be able to check on the heat when I'm not home, to control the system from our phones, and to create schedules for different rooms.

## Selecting a Brand

I looked at other systems from [Danfoss](https://store.danfoss.com/en/Climate-Solutions-for-heating/Hydronic-floor-heating/Service-kits-for-hydronic-floor-heating/Floor-Heating-Controls%2C-Danfoss-Link%E2%84%A2%2C-Master-Controller%2C-230-V%2C-24-V%2C-Number-of-channels%3A-10/p/014G0100) (more modern than our existing system), [Wunda](https://www.wundagroup.com/water-underfloor-heating/underfloor-heating-thermostats-controls/), and more. There were even some [smaller companies](https://logic-group.com/vare/zif5031/?lang=en) with some cool looking DIY solutions.

I didn't like any solution where I would have to go through a supplier or contractor to install the system (or even to get a manual!). I also wanted something built well from a proper company, not a "built-in-a-garage" gadget with limited support.

That's why I was happy to to come across the [HomematicIP](https://homematic-ip.com/en) ecosystem from German company eQ-3. They have a wide range of climate control devices for all sorts of heating systems (230V, 24V, wired, wireless, etc.). They also have a collection of other devices if I ever want to expand the system into other smart areas like light controls, security devices, air quality sensors, and more.

[{% picture jpt-webp /files/heating/HomematicIPOfferings.png --alt HomematicIPOfferings %}](https://homematic-ip.com/en/products-heating-and-climate-control?f%5B0%5D=category:66&page=,,,,,,,,,,1)

I greatly appreciate how they embrace empowering the owner. Every device is provided with detailed manuals, they publish YouTube videos demonstrating the components, and devices are readily available directly for the consumer through retailers like Amazon.nl. Additionally, there is an avid [community of HomematicIP users](https://homematic-forum.de/forum/), meaning there is a great deal of support if you need it!

Finally, I love the multiple options provided for controlling one's data using the system. You have the option to use the secure, anonymized German cloud system, or to run the system completely locally. Both options are fully supported by the manufacturer, and that feels rare in this age of data mining and limited customer rights.

## Device Selection

If there is a downside to the HomematicIP ecosystem, it's _**choice**_.

There are many types of underfloor heating controllers, thermostats, central control units, and more to choose from with the system. I'll go through the basics of why I chose what I did, but here's the list of components up front. I purchased my items from Amazon.nl and [Smart Home Supply](https://www.smarthomesupply.nl/). Obviously, the number of valve actuators that you need will depend on the number of heating loops that you have.

I haven't included any sort of contractor costs like an electrician or HVAC technician; if you feel comfortable wiring up an electrical socket, I think that you will feel comfortable doing this job yourself. Otherwise, a technician or handyman could probably complete the [mechanical installation](/heating/mechanical-installation) in about an hour.

| item                                                                      | qty | price per [EUR] | total [EUR] |
| ------------------------------------------------------------------------- | --- | --------------- | ----------- |
| [Access Point](https://www.amazon.nl/dp/B00ZQG6MGO)                       | 1   | 50              | 50          |
| [Thermostat](https://www.amazon.nl/dp/B01KPM3OQ4)                         | 3   | 50              | 150         |
| [Motorized Valve Controller](https://www.amazon.nl/dp/B07RJZ57D7)         | 1   | 200             | 200         |
| [Motorized Valve Actuator](https://www.amazon.nl/dp/B07RJZ5F1Y)           | 7   | 20              | 140         |
| [Switch Actuator HmIP-WHS2](https://www.amazon.nl/dp/B0758L1267)          | 1   | 70              | 70          |
| \*[Radiator Thermostat](https://www.amazon.nl/dp/B0C28SP75P)              | 1   | 55              | 55          |
| \*[Radiator Thermostat Adapter](https://www.amazon.nl/dp/B002KI3OFI?th=1) | 1   | 10              | 10          |
| Total                                                                     |     |                 | 675         |

\* _For an apples-to-apples comparison, ignore the radiator thermostat and adapter. The old Danfoss system did not control the heat in the bathroom, but we can do so easily with this new system._

### Wired vs Wireless

The HomematicIP system gives you the option of wired or wireless devices. Think of this as the data network for the devices. Given that we're retrofitting an existing home and not specifying a new build, I of course went with the wireless option. This will use the same 868MHz spectrum as the old Danfoss system (but don't fret, there's a solution for range concerns!). This helps us narrow down the types of thermostats and underfloor heating controllers.

### 24V vs 230V vs Motorized

Next, there are three types of underfloor heating controllers: 24V, 230V, and Motorized. Like our old 24V Danfoss system, the 24V and 230V systems refer to how the heating controller controls its valves. In these systems, the controller applies either 24V or 230V across the valve actuator and uses PWM (Pulse Width Modulation) to set "how open" the valve is. This is _fine_, but the motorized system has some benefits.

The motorized system is the newest from Homematic. Instead of featuring valves that require constant power to stay open, these valve actuators use a tiny servo motor to open and close the valve different amounts. With this approach, the valve actuator only draws power when it's actually opening or closing.

Now, in practice, this is a minor amount of power savings (maybe a kWh every couple of weeks), but I also think it's a better installation experience than the 24V or 230V valve systems.

The only benefit of choosing a 24V system is that there's a chance you could reuse the old Danfoss valve actuators (do so at your own risk!).

### Cloud vs Local Control

Finally, here's the biggest decision to make for the system configuration: do you want to control the system locally or via the cloud?

Even that one sentence is a bit of an over simplification. The cloud option of course allows local control via your thermostats, but uses the cloud for system configuration, smart phone control, and remote access. If you lose internet access at your house, you won't be able to control the system via your smartphone, but you can still use the thermostats as normal. In other words, if you lose internet at the house, the system will behave just the same as the old Danfoss system.

To keep things simple, I'll summarize the choice like this:

| Cloud                               | Local                                  |
| ----------------------------------- | -------------------------------------- |
| for the average homeowner           | for the smart home enthusiast / techie |
| cheaper                             | (likely) more expensive                |
| easiest set up                      | more complicated set up                |
| (probably) does everything you need | greatest flexibility                   |

I started with the Cloud option because it's the easiest to set up and test, and it's what I figured my neighbors with the same Danfoss system would be most interested in. I plan to change in the future to a Local system because, frankly, the smart home enthusiast in me wants to learn more about how things work.

### Selected System

And here's what the system architecture looks like. I'll call out a few key differences to the Danfoss system here.

[{% picture jpt-webp /files/heating/HomematicDiagramAccessPoint.png --alt HomematicDiagramAccessPoint %}](/files/heating/HomematicDiagramAccessPoint.png)

First, you'll notice that the underfloor heating controller does not communicate with the CV. It seems that the HomematicIP system's philosophy is to separate functions as much as possible. Perhaps this keeps down individual unit costs and allows for maximum flexibility? I'm not sure. Anyways, you need a separate unit to tell the CV to turn on and provide heat. It's basically a set of wirelessly controlled relays.

Second, you'll notice that the thermostats and the switching unit do not communicate with the heating system controller directly. Instead, all wireless communication goes through the main "brain", the Access Point.

This has some pros and cons. On one hand, this introduces another point of failure into the system. On the other hand, you may be able to place the Access Point in a more central location in your home - now the thermostat in your far-off bedroom doesn't need to reach all the way to the heating system controller, it just needs to reach the Access Point. It also makes the set up / pairing process much easier than the old Danfoss system.

## Next Steps

Next up, the [mechanical installation](/heating/mechanical-installation)!

{% picture jpt-webp /files/heating/HomematicProductStack.png --alt HomematicProductStack %}
