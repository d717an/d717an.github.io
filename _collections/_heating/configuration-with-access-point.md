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

In this post, we'll configure the new system using the HomematicIP app. Starting with the Access Point, everything is added to the system using device IDs included in the packaging of your devices (and on stickers attached to the devices).

## Get the App

First, install HomematicIP app onto your phone. Data is anonymized through your Access Point ID, so you don't need to create an account!

## Set Up the Access Point

- 5 minutes
- Follow the app's instructions
- Can take a few minutes for the light to go blue after connecting to your network via ethernet
- Should finish successfully, and then will probably download some updates
  - Flashing orange light and a message on the app will tell you it's installing updates
  - Should have a solid blue light once the updates are complete (needs a few minutes)
  - The brightness of the LED can be controlled from the app, and it can be turned off completely

## Switch Actuator for Heating System (WHS2)

- Click the "... More" button in the bottom right
- Click "Add device"
- If the unit doesn't appear, push the button on the switching actuator to activate pairing mode
- The final digits of the SGTIN can be found on the rear edge of the device or on the QR code sticker in the manual
- Add a room as necessary for the device (e.g. "CV Room")
- Give a name to the device or keep the default
- Configure the device
  - You can always modify this later
  - Select OUT (1)
    - This is the Normally Open (NO) switch with two terminals
    - For "Choose Function", select **"Switches an output for e.g. boiler or pump depending on the heating or cooling demand"**
    - For "Allocate the function", select **"Heating system control for heating and cooling requirements for underfloor heating controllers"**
    - This will automatically close the relay for OUT (1) when any zone in the underfloor heating controller calls for heat
  - Continue (you don't need to put anything on OUT (2))

## Motorized Underfloor Heating Controller

- Click the "... More" button in the bottom right
- Click "Add device"
- If the controller doesn't show up / the button isn't flashing orange any more, push the button on the underfloor heating controller to activate pairing mode
- Make / select a room (e.g. "CV Room")
- Give it a name
- Configure the device
  - Each circuit is for a valve
  - For example, let's connect circuit (1) to our "Living Room"
  - Select circuit (1)
  - Select room "Living Room"
    - This will pair the valve to the thermostat in the room; if the thermostat calls for heat, the underfloor heating controller will turn on the valve
  - Give the circuit or leave it as the default (I left it as the default name)
  - Set up the remaining circuits that have valves
  - Continue / finish the set up

### Troubleshooting

#### Heating zone error, adjustment range too small, check if valve pin is stuck

- I got this when I powered on a valve before attaching it to the manifold and it started calibrating itself
- In the app
  - Click the "... More" button in the bottom right
  - Click "Device Overview"
  - Press and hold the heating controller
  - Press "Reset"
  - Remove power from the heating controller
  - Install all the valves on the manifold, then into the controller, then power on the heating controller and let it calibrate the valves

#### Heating doesn't turn on immediately

- issue with safety thermostat?

## Wall Thermostats

### Hardware

- Pull thermostat out and away from its bracket
- Remove plastic tab breaking the battery circuit
- Install the grey plate on the wall
  - The hole pattern should match any mounting holes for the existing Danfoss thermostats (standard 55mm electrical boxes)
  - I found 3mm countersunk screws fit the wall plate nicely
  - There are also adhesive stickers in the manual if you need or prefer

### In the App

- Click the "... More" button in the bottom right
- Click "Add device"
- If the thermostat doesn't show up / the button isn't flashing orange any more, push the button with a blue rectangle on the thermostat to activate pairing mode
- The thermostat should show up in the app
- The app will ask for the last four digits of the SGTIN
- You can find them bolded on the QR sticker, or you can remove one of the batteries in the device to find the digits, write them down, and restart the pairing procedure
- Add a room to the app for where the thermostat will live (e.g. "Main Bedroom")
- Select the room
- Give the device a name (e.g. "Main Bedroom Thermostat")

## Bathroom Thermostat

Install the thermostat, let it calibrate. You may need to change the plunger length

### In the App

- Click the "... More" button in the bottom right
- Click "Add device"
- If the thermostat doesn't show up / the button isn't flashing orange any more, push the button with a blue rectangle on the thermostat to activate pairing mode
- The thermostat should show up in the app
- The app will ask for the last four digits of the SGTIN
- You can find them bolded on the QR sticker, or you can remove one of the batteries in the device to find the digits, write them down, and restart the pairing procedure
- Add a room to the app for where the thermostat will live (e.g. "Main Bedroom")
- Select the room
- Give the device a name (e.g. "Main Bedroom Thermostat")

## Additional Configuration in the App

- Congrats, you're done!
- It's worth testing each room to make sure it successfully calls for heat

### Emergency Operation Heating

- In the app, select the "... More" button in the bottom right
- Select "Device overview"
- Select the "Floor heating controller" (you may have renamed it)
- Under the "Device configuration" section, select "Emergency operation heating"
- From the app,
  - "The valve opening duration is recalculated every 15 minutes. If the radio communication between the wall thermostat and the floor heating controller fails for a longer period of time (e.g. if a battery is empty), the valves are controlled automatically. When the radio communication is recovered the system changes back to normal operation"
- My app had this value defaulted to 15%
- I changed it to 0% so that the CV does not unnecessarily heat our home; it's very well insulated and has never dropped below 15C even with the heating off

### Schedules

- By default, my thermostats were set to a "Standard schedule" (visible on the app home screen under each room)

#### Change to Manual Control (i.e. no schedule)

- To change this to Manual (what my Danfoss thermostats were, effectively), select the room in the app, then select "Standard schedule"
- Select "Manually" from the list, then select OK

#### Adjust Schedules

- Alternatively, if you like having a schedule, you can adjust them
- In the app, select the "... More" button in the bottom right
- Select "Heating schedules" under the Climate control section
- Here you can adjust the "Standard schedule" for each room individually
- You can also select "Adjust Visibility" to show some hidden schedules for each room in case you want to have multiple schedules for each room
- Only one schedule can be active for a room at a time, but it's easy to switch between them
- can do on the thermostat as well by pressing and holding the selection wheel

## Additional Testing

### What Happens if the House Loses Internet?

- Without a home internet connection, I could not control the heating system from my phone
- However, heating schedules and thermostats functioned normally
- In other words, without a home internet connection, the system operated exactly the same as the previous Danfoss system

## Future Work

This is a list of things I'm going to do in the future to further enhance the heating system.

### Power Supplies for Wall Thermostats

- 50 eur each
- Homematic IP makes a 230VAC power supply for the battery powered thermostats
  - https://homematic-ip.com/en/product/power-supply-unit-brand-switches
- With this, you can add this into your wall next to a light switch or outlet and power your thermostats continuously from the mains, no batteries needed
- Obviously, this is much more involved than just batteries, but nice to have the option!

### Change Access Point to Local Control

- 75 - 150 eur
- The rest of our smart home is controlled via local APIs via Home Assistant
- Homematic's Access Point is an excellent and affordable way to get a modern heating system into the apartment
- However, I'd like more local control, and I'm comfortable managing our own external access to the home
- With that, I'll eventually switch to Homematic IP's other options for the "central brain", either the CCU3 or the community's open source RaspberryMatic
