---
layout: post
title: "HomematicIP Heating System - Configuration with Access Point"
description: >-
  I set up our new HomematicIP Heating System for the first time using the cloud approach. In other words, I configure the system with the smartphone app and the Acccess Point
date: 2025-01-28
order: 30
toc: true
---

_This is a post in a series of blogs about upgrading our underfloor heating system; here's the [first post in the series](/heating/selecting-a-new-heating-system) if you'd like to start at the beginning._

## Summary

In this post, we'll configure the new system using the HomematicIP app. I'll then describe some quick tests I did to see how the system behaves.

Starting with the Access Point, everything is added to the system using device IDs included in the packaging of your devices (and on stickers attached to the devices). You will create rooms via the app and assign your devices to the rooms.

Each new device will need to be put into pairing mode so that the Access Point can add it to your system. If you're just turning things on for the first time, they should automatically enter pairing mode. If that doesn't happen or you've already powered things on, each devices' manual will have instructions on how to re-enter pairing mode (usually this involves pressing and holding the button with the blue square on the device).

## Get the App

First, install HomematicIP app onto your phone. Data is anonymized through your Access Point ID, so you don't need to create an account!

![ipLogo](/files/heating/ipLogo.png)

## Set Up the Access Point

The Access Point comes with an AC power adapter and an ethernet cable. Remember that all of your devices will connect to this unit, so it's best to keep it as centrally located in your home as possible. However, it needs to be connected to your internet via ethernet. If you do not have connected ethernet ports around your house, the easiest thing to do is to install it near your router.

The app will walk you through the set up process. It can take a few minutes for the light to go blue after connecting to your network via ethernet. After it's connected to the HomematicIP cloud, it will probably need a few more minutes to install some updates - the status LED will flash orange and there will be a message on the app. You can also change the brightness of the Access Point LED via the app, which is great if you have it out on a TV console like I do.

![Screenshot_AccessPoint](/files/heating/Screenshot_AccessPoint.png)

Now that the central "brain" of the system is set up on the app, you can start adding the rest of your devices. We'll start by activating all of our thermostats. This way, we'll have rooms and sensors set up in the app, and we'll be able to assign heating outputs to them.

## Wall Thermostats

The wall thermostats come with three pieces: an outer frame, a gray mounting plate, and the actual thermostat. The thermostat clips into the gray mounting plate, pinching the outer frame between the two. To disassemble, just pull the thermostat out and away from the other pieces. Now you can remove plastic tab breaking the battery circuit. The device's button will start flashing orange to show that it's in pairing mode. You can always get the device back into pairing mode later.

To add the thermostat to the app, you'll need the last four digits of its SFTIN (i.e. its ID code). You can find them bolded on the QR sticker included in the device's manual, or you can remove one of the batteries in the device to find the digits on a sticker attached to the device. Write them down for use later.

The thermostat can be mounted to the wall using the grey plate. Alternatively, my thermostats also came with some double sided tape if you want to stick them to the wall. There are also [desk / table mounts](https://www.amazon.nl/-/en/Homematic-Holder-Accessory-Devices-141743A0/dp/B011U6591W/) if you don't want to mount the thermostat to the wall. I mounted mine to the wall, and I found the hole pattern matched the mounting holes for the old Danfoss thermostats (standard 55mm electrical boxes). 3mm countersunk screws fit the wall plate nicely.

![WallThermostat](/files/heating/WallThermostat.png)

### In the App

- Click the "... More" button in the bottom right
- Click "Add device"
- If the thermostat doesn't show up / the button isn't flashing orange any more, push the button with a blue rectangle on the thermostat to activate pairing mode
- The thermostat should show up in the app
- The app will ask for the last four digits of the SGTIN that you found earlier (QR code sticker on the device or from the manual)
- Add a room to the app for where the thermostat will live (e.g. "Main Bedroom")
- Select the room
- Give the device a name (e.g. "Main Bedroom Thermostat")

Repeat for all of your thermostats.

## Bathroom Thermostat

With all actuators like radiator thermostats and heating manifold valve actuators, they start a calibration process as soon as they get power for the first time. With that in mind, it's best to install them _first_, then give them power for the first time. You shouldn't need any tools to install the thermostat onto the valve adapter on the radiator. What I found worked best for me was to screw the thermostat on by hand with the screen of the thermostat pointing up. Then, when I couldn't snug up the nut any further, I rotated the body of the thermostat another 45 degrees away from the wall, snugging up the nut and making the screen easier to see.

![RadiatorThermostat](/files/heating/RadiatorThermostat.png)

Now that the body of the thermostat is installed, you can remove the battery cover, install batteries, and power on the device. You may hear the motor start moving as it trains the device on the location of the valve.

### In the App

- Click the "... More" button in the bottom right
- Click "Add device"
- If the thermostat doesn't show up / the button isn't flashing orange any more, push the button with a blue rectangle on the thermostat to activate pairing mode
- The thermostat should show up in the app
- The app will ask for the last four digits of the SGTIN (QR code sticker included in the manual)
- Add a room to the app for where the thermostat will live (e.g. "Bathroom")
- Select the room
- Give the device a name

### Troubleshooting

If you see errors on the thermostat like "F1", "F2", or "F3", you have a mechanical problem with the mounting of the thermostat. The thermostat can't actuate the valve correctly. The app should tell you more specifics about the problem, such as "range too small", "range too big", or "stuck pin". Basically, the actuator isn't encountering the resistance it expects when it tries to actuate the valve. Check these things:

- Is the thermostat screwed on to the adapter all the way?
- Is the valve adapter screwed on to the radiator valve all the way?
- Did you include a plunger between the thermostat and the valve adapter?
- Does the plunger stick out of the adapter about 5-10 mm?

![RadiatorAdapterPlunger](/files/heating/RadiatorAdapterPlunger.png)

## Switch Actuator (WHS2)

Now that our thermostats and rooms are set up, we can configure the CV room. First, plug in the switch actuator that you worked so hard on!

### In the App

- Click the "... More" button in the bottom right
- Click "Add device"
- If the unit doesn't appear, push the button on the switch actuator to activate pairing mode
- The final digits of the SGTIN can be found on the rear edge of the device or on the QR code sticker in the manual
- Add a room as necessary for the device (e.g. "CV Room")
- Give a name to the device or keep the default

We'll now configure the device by telling it what we want the different outputs to do. If you aren't installing a bathroom thermostat, you don't need to worry about Output 2. You can always modify this later.

- Select OUT (1)
  - This is the Normally Open (NO) switch with two terminals
  - For "Choose Function", select **"Switches an output for e.g. boiler or pump depending on the heating or cooling demand"**
  - For "Allocate the function", select **"Heating system control for heating and cooling requirements for underfloor heating controllers"**
  - This will automatically close the relay for OUT (1) when any zone in the underfloor heating controller calls for heat
- Select OUT (2)
  - This is the relay with a common, a NO, and a NC terminal
  - For "Choose Function", also select **"Switches an output for e.g. boiler or pump depending on the heating or cooling demand"**
  - For "Allocate the function", select **"Heat demand for rooms - control for selected rooms with radiator thermostats"**
  - Select the room with your radiator thermostat (e.g. "Bathroom")
  - I turned off Emergency Mode as I'm not worried about the bathroom every freezing if the radiator thermostat signal is lost

## Motorized Underfloor Heating Controller

Finally, plug in your underfloor heating controller. You'll start hearing the valves calibrate. This can take 5-10 minutes as each valve sequentially repeats its calibration a few times. If you see any errors above any of the zone numbers on the controller, you may have to reseat that valve actuator onto it's valve adapter.

### In the App

- Click the "... More" button in the bottom right
- Click "Add device"
- If the controller doesn't show up / the button isn't flashing orange any more, push the button on the underfloor heating controller to activate pairing mode
- Make / select a room (e.g. "CV Room")
- Give it a name

To configure the device, we need to assign each heating circuit to the room it heats. You should now have thermostats in each of these rooms that will then activate the underfloor heating controller. In my case, I have heating circuits 1-4 assigned to "Living Room, circuits 5-6 assigned to "Main Bedroom", and circuit 7 assigned to "Second Bedroom". Go through the configuration and assign all the circuits to rooms.

## Time to Test!

Congrats, you're done! Now you can test each room to make sure it successfully calls for heat. I recommend doing it from the actual thermostat first, then also testing control from the app.

Keep in mind that the radio system is not "instant" - it may take a minute for the thermostat to send a message to the Access Point, and then to the underfloor heating controller and switch actuator.

For each room, confirm the following:

**Is the underfloor heating controller opening the correct valves?**

This can be verified on the underfloor heating controller display.

**Is the switch actuator calling for heat?**

If you're testing control via the app, you can stay in the CV room, and you should be able to hear the _**click**_ of the relay(s).

**Is the CV supplying hot water?**

My CV shows a "50" on its display when it enters heating mode (for 50C water as opposed to 60C water for Domestic Hot Water like showering). My CV can only supply _either_ heating water or domestic hot water, and domestic hot water takes priority, so make sure no one is showering or doing the dishes while you're testing. Note that this also means you can't heat your bathroom radiator while showering!

## Configure "Emergency Operation" Heating

One major complaint about the old Danfoss system was that it would enter an over-powerful emergency heating mode if any of the thermostats dropped off the network. The HomematicIP system has a similar mode, but you can configure it through the app.

### In the App

- Select the "... More" button in the bottom right
- Select "Device overview"
- Select the "Floor heating controller" (you may have renamed it)
- Under the "Device configuration" section, select "Emergency operation heating"
  - "The valve opening duration is recalculated every 15 minutes. If the radio communication between the wall thermostat and the floor heating controller fails for a longer period of time (e.g. if a battery is empty), the valves are controlled automatically. When the radio communication is recovered the system changes back to normal operation"
- My app had this value defaulted to 15%
- I changed it to 0% so that the CV does not unnecessarily heat our home; it's very well insulated and has never dropped below 15C even with the heating off

## Scheduling

A major benefit of the new system is its easy-to-configure scheduling. By default, my thermostats were set to a "Standard schedule" (visible on the app home screen under each room). You can have up to three schedules per room, or you can keep them in manual control.

### Adjust Schedules in the App

- Select the "... More" button in the bottom right
- Select "Heating schedules" under the Climate control section
- Here you can adjust the "Standard schedule" for each room individually
- You can also select "Adjust Visibility" to show some hidden schedules for each room in case you want to have multiple schedules for each room
- Only one schedule can be active for a room at a time, but it's easy to switch between them
- You change schedules on the thermostats as well by pressing and holding the selection wheel
- Select "Manual" if you only want to change the thermostats yourself

## Test - Loss of Internet

Obviously, losing internet is a concern with a cloud based system. I confirmed that without a home internet connection, I could still control my heat with my thermostats. However, since all of the app functionality uses the cloud, I could not control the heating system from my phone. In other words, without a home internet connection, the system operated exactly the same as the previous Danfoss system
