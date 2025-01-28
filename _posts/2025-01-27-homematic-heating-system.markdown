---
layout: post
title: "Replacing a Danfoss Underfloor Heating System with Homematic IP"
date: 2025-01-27 08:00:00 +0100
categories: smart-home homematic heating
---

# Why?

## Why Replace The Existing System?

- I wanted several features from my heating system
  - Scheduling
  - Smart home compatibility
  - Ability to check on and control the heating when away home
  - Smart phone compatibility
  - Resiliency to wireless thermostat compatibility (in other words, stop the system from turning on when it loses contact with a thermostat)

## Why Homematic IP?

- I looked at other systems from Danfoss, WTH, and more
- I settled on the German company, Homematic, for several reasons
  - They have an impressive ecosystem of components if I want to add devices later like
    - radiator thermostats
    - door / window sensors
    - light switches
    - etc.
  - Their system is compatible with switching between heating and cooling modes (in case our building ever installs a cold water supply for cooling)
  - They have multiple options for controlling the system
    - A secure, anonymized cloud in Germany, or
    - Complete local control, or
    - Strong open-source community support for the "RaspberryMatic" project
  - They have a strong user base in Germany with many forum posts, YouTube videos, etc. - great for the DIY-er!
  - Their products are readily available from retailers in the Netherlands

# Purchases

- All components were purchased from Amazon.nl
- Another supplier I found: https://www.smarthomesupply.nl/

| item                       | qty | price per [EUR] | total [EUR] | Source                                           |
| -------------------------- | --- | --------------- | ----------- | ------------------------------------------------ |
| Access Point               | 1   | 50              | 50          | [amazon.nl](https://www.amazon.nl/dp/B00ZQG6MGO) |
| Thermostat                 | 3   | 50              | 150         | [amazon.nl](https://www.amazon.nl/dp/B01KPM3OQ4) |
| Motorized Valve Controller | 1   | 200             | 200         | [amazon.nl](https://www.amazon.nl/dp/B07RJZ57D7) |
| Motorized Valve Actuator   | 7   | 20              | 140         | [amazon.nl](https://www.amazon.nl/dp/B07RJZ5F1Y) |
| Switch Actuator HmIP-WHS2  | 1   | 70              | 70          | [amazon.nl](https://www.amazon.nl/dp/B0758L1267) |
| Total                      |     |                 | 610         |                                                  |

# Installation with Access Point

## Get the App

- Install Homematic IP app
- No log in / account needed, data is anonymized with the access point ID

## Set Up the Access Point

- 5 minutes
- Follow the app's instructions
- Can take a few minutes for the light to go blue after connecting to your network via ethernet
- Should finish successfully, and then will probably download some updates
  - Flashing orange light and a message on the app will tell you it's installing updates
  - Should have a solid blue light once the updates are complete (needs a few minutes)
  - The brightness of the LED can be controlled from the app, and it can be turned off completely

## CV Room Prep

- 20 min

### Power Down the Existing System

- Unplug your CV
- Unplug your existing underfloor heating system (Danfoss CF-MC 071CU-02B-24) in my case

### Record Your Existing Zones

- Your heating manifold will have several heating circuits, each with a control valve
  - In my case, I have eight heating circuits with seven control valves
  - The eighth is left permanently open because it's controlled with a radiator thermostat in the bathroom, hence no valve needed
- You'll want to know which room each circuit supplies for setting up the homematic system, so figure that out now and write it down
- Take lots of pictures!
- Due to power limitations on each zone, my Danfoss system had four zones configured to control three rooms in the house using seven valves, aka circuits (confusing, right??)
  - Zone 1, 2
    - Valves 1, 2, 3, 4
    - Living room and kitchen
  - Zone 3
    - Valves 5, 6
    - Main bedroom
  - Zone 4
    - Valve 7
    - Second bedroom
  - Circuit 8
    - No zone
    - No control valve (permanently open)
    - Main bathroom, controlled with a radiator thermostat
    - Only gets heat if another zone is calling for heat
- Thankfully, the installer also wrote down a room designation underneath each valve on the supply (blue) manifold

![Pasted image 20250127095741.png](/files/Pasted image 20250127095741.png)

- They joined multiple valves into single zones using a terminal block inside a junction box
  - Don't worry, the new system is much simpler and does not need this wiring!

![Pasted image 20250127095940.png](/files/Pasted image 20250127095940.png)

### Remove the CV Signal Wires

- **WARNING** (again) make sure the CV is unplugged, and always best to confirm there is no voltage across the signal wires
  - In my case, the CV provides 24VDC to the Danfoss system
  - When the Danfoss system calls for heat, it closes a relay, providing this 24VDC back to the CV, and this in turn activates the heating mode of the CV
  - 24VDC is not particularly dangerous, but you don't want to cause inadvertent damage to you or your CV, so best to unplug the CV!
- We need to separate out the wires to the CV for reuse with the new heating control system
- In my case, I basically pulled out the black two-conductor low voltage wire
  - One end went to a contact thermostat clipped to the hot water supply line
  - Another went to the CV
  - The final end went to the relay control on the Danfoss
- I also removed the control signal from the Danfoss controller (black wire on the left) using a small flat head screwdriver to push on the orange tabs above the terminals while pulling the wires away from the unit

![Pasted image 20250127103540.png](/files/Pasted image 20250127103540.png)

### Unmount Old Underfloor Heating Controller

- Now that the CV control signal is separated from the old heating controller, the entire system can be removed
- Remove the old valves
  - There is a button / lever on the front of the valves
  - Press and hold this button, then pull the valve up
- Unscrew the old valve adapters and remove from the manifold
- Unscrew the old heating controller from the wall
- Save the system or recycle it (e.g. at Praxis)

### Optional - Add Mounting Board

- This is optional; you can also install directly into the masonry wall
- To make mounting devices easier (screwing into wood instead of masony), I purchased a 61cm x 122cm 18mm underlayment board from Praxis (local hardware store)
  - This matches the plywood already installed on the wall that the underfloor heating manifold
  - The store trimmed it to 61cm x 40cm for me
  - I put a few coats of white paint on it so it blended in to the wall
  - I then fixed it to the masonry wall directly above the plywood used for the heating manifold, giving me a large wooden surface to fix the devices too

![Pasted image 20250127094250.png](/files/Pasted image 20250127094250.png)

## Switch Actuator for Heating System (WHS2)

- 30 minutes

### Hardware

- **WARNING**
  - Refer to the manual carefully for this
  - Do not proceed if you are not comfortable working with 230V
  - Only work on the connections with power removed from the unit
  - Do the "tug test" after securing cables to make sure they are indeed secure
  - Triple check your connections
- **Unplug the CV**
- **Ensure the plug you're wiring into the switching actuator is not plugged in while you're working on it**
- Loosen the screws on the bottom back of the switching actuator unit (they do not need to be removed completely)
- Gently pull the front door down, then away from the unit at the bottom edge, it should come free
- With a sharp utility knife or pair of pliers, remove the left and right-most bushing openings from the bottom rear of the actuator
- Gently remove the left and rightmost strain relief clamps
- Install power on the left hand side with L, N, and earth connections
- Install the 24VDC connection from the CV into Output (1)
- Reinstall the strain relief clamps, ensuring a snug fit on the wires
  - I used a few wraps of electrical tape on my power cable to ensure a snug fit
- I installed a small electrical box beneath the switching actuator to hold my lever nuts
- My CV was wired with a safety cutoff thermostat switch clipped to the hot water supply of the underfloor heating system

![Pasted image 20250127091907.png](/files/Pasted image 20250127091907.png)

- It is wired in in series with the hot leg of the 24VDC signal from the CV
  - My guess is if the hot water pipe gets too hot, this thermostat opens, breaking the connection to the CV and turning off the demand for hot water
- Anyways, I preserved that connection, and here is how I wired things up

![Pasted image 20250127091050.png](/files/Pasted image 20250127091050.png)

![Pasted image 20250127093316.png](/files/Pasted image 20250127093316.png)

- Finish the installation by mounting the device to the wall
- Mount the junction box to the wall
- Replace the cover of the switching actuator and junction box
- Plug the switching actuator into power
- The unit's light should intermittently flash

### In the App

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

- 15 minutes

### Hardware

- Attach the underfloor heating controller to the wall above your heating manifold
  - Leave enough vertical space to cable manage your valve wires and the controller's power cord (I left about 20-25cm of space)
- **Install your valves onto the manifold before plugging in the valves to the controller and powering on the controller**
  - As soon as the valves first get power, they start a calibration process and need to be attached to your manifold
- Install the new valve adapters
  - **Be careful, they should screw on very easily**
  - If they're not screwing on, you probably are slightly misaligned, just keep trying
  - Make sure the valve adapters are finger-snug - no tools are needed to tighten them
- Install the valves on the valve adapters
  - **Ensure the valves fully "click" on!**
  - You don't want the valves popping off
- Plug the valves into the underfloor heating controller in order (i.e. left-most valve goes into heating zone 1, second-left-most valve goes into heating zone 2, etc.)
- Plug in the underfloor heating controller
- The display should come on, and you will likely hear the valves start moving as they calibrate to find the max open and closed positions
- This calibration process may take 5-10 minutes depending on how many valves you have

### In the App

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

## Thermostat (x3)

- 5 minutes

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

## Additional Testing

### What Happens if the House Loses Internet?

- Without a home internet connection, I could not control the heating system from my phone
- However, heating schedules and thermostats functioned normally
- In other words, without a home internet connection, the system operated exactly the same as the previous Danfoss system

# Future Work

This is a list of things I'm going to do in the future to further enhance the heating system.

## Bathroom Smart Thermostat

- 35 - 50 eur
- Homematic IP makes a range of battery powered smart radiator thermostats
- I'm going to replace our existing TRV radiator valve in our bathroom with one of these thermostats so that we can independently heat our bathroom without needing one of the heating zones to call for heat

## Power Supplies for Wall Thermostats

- 50 eur each
- Homematic IP makes a 230VAC power supply for the battery powered thermostats
  - https://homematic-ip.com/en/product/power-supply-unit-brand-switches
- With this, you can add this into your wall next to a light switch or outlet and power your thermostats continuously from the mains, no batteries needed
- Obviously, this is much more involved than just batteries, but nice to have the option!

## Change Access Point to Local Control

- 75 - 150 eur
- The rest of our smart home is controlled via local APIs via Home Assistant
- Homematic's Access Point is an excellent and affordable way to get a modern heating system into the apartment
- However, I'd like more local control, and I'm comfortable managing our own external access to the home
- With that, I'll eventually switch to Homematic IP's other options for the "central brain", either the CCU3 or the community's open source RaspberryMatic
