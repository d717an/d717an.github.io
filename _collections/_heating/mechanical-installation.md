---
layout: post
title: "HomematicIP Heating System - Mechanical Installation"
description: >-
  Installing the underfloor heating controller, valves, and CV switch for a new Homematic IP heating system
date: 2025-01-27
order: 20
toc: true
---

_This is a post in a series of blogs about upgrading our underfloor heating system; here's the [first post in the series](/heating/selecting-a-new-heating-system) if you'd like to start at the beginning._

## Summary

In this blog, I'll share the mechanical and electrical details of replacing our ~10 year old Danfoss underfloor heating controller with a new HomematicIP system. I'll describe powering things on and configuring them in the app (i.e. via the Access Point) in the next blog post.

A couple warnings before we start.

### Electrical Safety

These steps involve wiring up systems to 230V mains voltage. If you've ever wired up an outlet or a switch, it will be no different. Use best practices like powering down everything you're working on, confirming there's no power before touching any wires, ensuring all electrical connections are snug and properly torqued down, using proper wire sizes for everything, etc.

This isn't a particularly scary or dangerous task, but just make sure you take the proper precautions to do things safely.

### Know Your CV

This system works for my CV (a 2013 Intergas Kombi Kompakt HRE 36/30) - make sure you know how your own CV works, what voltage it's putting out on its control wires, etc. In my case, my CV is supplying two wires to the CV: a 24VDC supply and a return signal wire. When the controller closes its relay and brings the return signal wire up to 24V, the CV enters its underfloor heating mode, supplying hot water to the underfloor heating system. The hot water then flows through any circuit with an open valve. Best to confirm with a multimeter or through the CV's manual that your CV functions the same.

## Document the Existing System

Before removing everything, take a minute to document the existing system. You'll need to be able to associate each heating circuit with the room it heats.

[{% picture jpt-webp /files/heating/ManifoldOld.png --alt ManifoldOld.png %}](/files/heating/ManifoldOld.png)

Your heating manifold will have several heating circuits, each with a control valve and valve actuator. In my case, I have eight heating circuits with seven control valves. The eighth circuit is left permanently open because it's controlled with a Thermostatic Radiator Valve (TRV) on the bathroom radiator, hence no valve is needed on the manifold.

Thankfully, either the installer or a previous owner grouped the heating circuits together with some permanent marker on the return manifold. I have four circuits in our living room and kitchen, two circuits for our main bedroom, one for the small bedroom, and one for the main bathroom radiator. Multiple circuits are used for bigger rooms to help balance how quickly different areas of the room heat up.

The old [Danfoss heating controller](https://store.danfoss.com/is/en/Climate-Solutions-for-heating/Hydronic-floor-heating/Service-kits-for-hydronic-floor-heating/Floor-Heating-Controls%2C-Master-Controller-CF2%2B%2C-230-0-V%2C-Number-of-channels%3A-5/p/088U0245) (model CF-MC, aka 088U0245, part number 071CU-02B-24) has a relay and can control up to five heating circuits.

[{% picture jpt-webp /files/heating/DanfossController.png --alt DanfossController.png %}](/files/heating/DanfossController.png)

Obviously, that doesn't work for seven heating circuits, so we get this lovely junction box where multiple valve actuators are merged into a single zone for the heating controller. Thankfully, the new system can control up to 12 zones, so no need mess around with valve actuator wiring! We will need to do some wiring, so you may want to keep this plastic junction box if it's good shape.

{% picture jpt-webp /files/heating/DanfossWiringMess.png --alt DanfossWiringMess.png %}

Here's how my system was ultimately configured:

- Zone 1, 2
  - Valves 1, 2, 3, 4
  - Living room / kitchen
- Zone 3
  - Valves 5, 6
  - Main bedroom
- Zone 4
  - Valve 7
  - Small bedroom

## Remove the Old System

:warning: **Once you start this process, you won't have heat until you finish installing and setting up the new system**. Best to read through all the blog posts in the series and to make sure you have everything you need (devices, materials from the hardware store, etc.).

Out with the old, in with the new!

### Remove the CV Signal Wires

:warning: Before starting, **power down / unplug both your CV and your heating controller**.

In my setup, there was only 24VDC across the CV control circuit, but probably best to avoid having live, exposed signal wires hanging around!

[{% picture jpt-webp /files/heating/DanfossControllerWireRemoval.png --alt DanfossControllerWireRemoval.png %}](/files/heating/DanfossControllerWireRemoval.png)

The only wires we need to remove from this system are those going to the CV. In the picture above, those are the ones on the far left going to the relay. Also separate out and keep the pipe-mounted thermostat:

{% picture jpt-webp /files/heating/20250127091907.png class="w75" --alt 20250127091907 %}

Each wire in the old Danfoss controller has little orange push tab above it that can be depressed with a small flathead screwdriver. While depressing the orange tab, pull the wire out and away from the controller.

### Remove the Old Valve Actuators

The old valve actuators will come off very easily; just push hard on the push tab on the front of the actuator, then pull it up and away from the valve. Then unscrew the plastic adapter piece from the metal valve.

[{% picture jpt-webp /files/heating/ValveActuatorRemoval.png --alt ValveActuatorRemoval %}](/files/heating/ValveActuatorRemoval.png)

### Remove the Old Heating Controller

Now that the CV control signal is separated from the old heating controller and the valve actuators are detached from the valves, you can remove the old heating controller from the wall. Save the system or recycle it (e.g. at Praxis).

## Optional - Add a Mounting Board

This is completely optional, but I prefer installing some plywood backing to the masonry, then installing everything onto the plywood. I find it a lot more forgiving to mount things with small screws into plywood rather than drilling into masonry and using anchors.

A 61cm x 122cm x 18mm underlayment board from Praxis (local hardware store) was less than 20 euros, and the store cut off a 61 x 40 cm piece for me. I put a few coats of white paint on it so it blended in to the wall, then fixed it to the masonry wall directly above the plywood used for the heating manifold with a few large anchors. I didn't take a picture before mounting the new heating controller, so here's a sneak peak of the finished installation.

{% picture jpt-webp /files/heating/20250127094250.png --alt  20250127094250.png %}

## Switch Actuator (WHS2)

The switch actuator is really just a set of two relays that can be controlled by the HomematicIP system. This box has two relays. "Output 1" has two terminals. When active, the two terminals are connected. "Output 2" is referred to as a "switching" output. All this means is that it has three terminals: a common, a Normally Closed (NC), and a Normally Open (NO). When not active, the common is connected to the NC terminal. When active, the common is connected to the NO terminal.

If choose the cloud configuration of the HomematicIP system, you can only assign an output to one kind of heating "demand" at a time. In HomematicIP terms, a heating demand is something like an underfloor heating controller _OR_ a radiator thermostat. Since I'm adding a radiator thermostat to our bathroom radiator, I'm going to have two types of heating demands, so I'm going to wire up _both_ outputs of the switch actuator.

### Before Starting

This is the most involved portion of installing the heating system yourself. Don't be intimidated though, it's not that bad. You'll need a few things from Praxis or your local hardware store:

- a mix of [two]() and [three way lever nuts]()
- an [electrical junction box]()
- a [power cord]()
- some [electrical tape](https://www.praxis.nl/gereedschap-werkplaats/handgereedschap/elektriciensgereedschap/elektrische-isolatietape/tesa-elektrische-isolatie-pvc-tape-zwart-15mm-10m/4453300)

I'm assuming you have some basic tools like a screwdriver and wire strippers (though a utility knife can strip wires in a pinch).

Just a reminder of what I said before...

- **Your CV should still be unplugged**
- **Ensure the plug you're wiring into the switching actuator is not plugged in while you're working on it**
- Refer to the manual carefully for this
- Do not proceed if you are not comfortable working with 230V
- Only work on the connections with power removed from the unit
- Make sure your connections are snug (give them the "tug test" after fastening them)
- Triple check your connections

### Wiring Schematic

Here's the wiring we're going for. This assumes a couple of things. First, I'm also wiring up Output 2 because I'm installing a radiator thermostat in addition to the underfloor heating controller. Second, my system already had a contact thermostat clipped on to the manifold supply line, so I'm keeping it in the system. Obviously, adjust your set up as needed.

[{% picture jpt-webp /files/heating/ActuatorWiringSchematic.png --alt ActuatorWiringSchematic %}](/files/heating/ActuatorWiringSchematic.png)

Here's how this works. The CV provides a 24VDC line (don't base your wiring off of color, my CV was wired up with blue as the 24V line) and a return wire. When the blue wire is brought up to 24VDC, the CV starts providing hot water to the heating pipework. With this wiring setup, either Output 1 our Output 2 can connect the return wire to 24V.

The contact thermostat acts as a switch in the system. I don't have the exact specs on this model, but I believe it's a model where it is normally closed (i.e. it does _not_ break the circuit) and opens when it detects a certain temperature. Mine was clipped to the supply, or hot side, of the heating manifold. If the contact thermostat switch is open, it will break the 24V supply from the CV, thus the CV will not provide hot water for the heating system.

**\*Since installing the system, I've noticed the contact thermostat prevent the CV from turning on a few times.** The CV is set to a consistent 50C output temperature for the underfloor heating, so I now think this contact thermostat should be clipped **to the return side of the manifold**. Therefore, it behaves as an efficiency switch - if the return water temperature from the underfloor heating is too hot, it means the floor is already up to temperature and is not taking enough heat. Therefore, the heating should be turned off.

### Installation

You can access the connection terminals and mounting holes of the switch actuator by loosening the screws on the bottom back of the switching actuator unit (they do not need to be removed completely). Gently pull the front door down, then away from the unit at the bottom edge, and it should come free. With a sharp utility knife or pair of pliers, remove the left and right-most bushing openings from the bottom rear of the actuator. Gently remove the left and rightmost strain relief clamps with a screwdriver and make your connections. I used a few wraps of electrical tape on my CV signal cable to ensure a snug fit with the strain relief clamp. My CV connection wire had a bunch of slack, so I cut off some of the slack and used it to make the second connection from the junction box to Output 2.

[{% picture jpt-webp /files/heating/WiredSwitchActuator.png class="w75" --alt WiredSwitchActuator %}](/files/heating/WiredSwitchActuator.png)

Check all of your connections are secure (i.e. tug test) and confirm everything is in the right place. Finish the installation by mounting the switch actuator to the wall. Mount the junction box to the wall. Finally, replace the cover of the switching actuator and junction box.

Don't power on the unit yet, we'll do that in the next blog post.

Congrats! If you got through that, the rest is easy.

## Underfloor Heating Controller

Don't power on the unit until we get to the next post - and definitely don't power on the system until all the valve actuators are installed because they start a calibration process as soon as they power on.

### Mounting

Attach the underfloor heating controller to the wall above your heating manifold. You can either mount it to a DIN rail or use screws. If you use screws, look at the back of the unit. There are sliding pieces of plastic made to grip the DIN rail. You can push those down to expose additional screw mounting points beneath the unit. Leave enough vertical space to cable manage your valve wires and the controller's power cord (I left about 20-25cm of space).

### Valve Actutators

First, install the new HomematicIP valve adapters onto the metal valves. **They should screw on very easily.** If you encounter any resistance, you're probably slight misaligned. Just keep adjusting the orientation of the valve adapter and try again. The adapters only need to be hand-snug - no tools are needed to tighten them.

Next, install the new HomematicIP motorized valve actuators onto the adapters. **Ensure the valves fully "click" on!**

Finally, plug the valves into the underfloor heating controller starting from the left. Cable manage to your heart's content! It should look something like this when you're done, though nothing will be on the screen, because we'll power things on and configure things in the next blog post.

{% picture jpt-webp /files/heating/WiredActuator.png --alt WiredActuator %}

## Bathroom Radiator Thermostat

Changing the bathroom thermostat only requires an adjustable wrench. Remove the existing radiator thermostat, gently loosening the nut with an adjustable wrench.

{% picture jpt-webp /files/heating/TrvRemoval.png --alt TrvRemoval %}

Unfortunately, the adapter I needed to bring my radiator's M28 thread size to the HomematicIP thermostat's M30 size wasn't included with the thermostat. The correct adapter was easily found on Amazon though. Screw on the adapter hand tight, and you can very gently snug it up with a wrench if you like. The adapter comes with a few plungers of different sizes - pick one that protrudes from the adapter body about five millimeters, like so. We'll add the actual thermostat after installing the Access Point in the next post.

{% picture jpt-webp /files/heating/AdapterInstalled.png --alt AdapterInstalled %}

## Next Steps

{% picture jpt-webp /files/heating/FinishedInstallation.png --alt FinishedInstallation %}

Finally, we'll [power on and configure the system](/heating/configuration-with-access-point) using the HomematicIP app!
