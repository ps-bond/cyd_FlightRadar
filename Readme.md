### CYD Flightradar

First pass at using a Cheap Yellow Display to integrate with Home Assistant's Flightradar24 integration (installed via HACS)
Displays a list of aircraft in area with (what I deemed as) relevant data.

## How to use

Import the contents of src/ into your ESPHome configs directory.  Install cyd-flightradar24.yaml to your CYD device.

## Current issues

Resource intensive - needs to mangle incoming Python data to JSON then parse as JSON.  Inefficient, looking at modifiying the integration to emit JSON instead.

Too much data exceeds stack.  Device is not stable and reboots under heavy load.  Solution is probably to create a template sensor on HA to limit the number of flight entries passed to the device.

Backlight levels - still tuning use of LDR to set backlight.  Broadly works, but could be better.

Currently displays LVL if the vertical speed is +/- 10 - check glider ascent/descent rates (esp. at launch) to see if this is reasonable.  

Display is updated every 15s - hugely inefficient, will move lambda contents to on_raw_event in the sensor: section instead.  Need to look at addressing the display component from the sensor block.
