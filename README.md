# ATS-25X2
My mods to the V.5.3b 17.09.2022 PE0MGB SI4735-Radio-ESP32-Touchscreen-Arduino



NOTE: See the source code for this note (and more information about where to get this - and other - files/libraries) -
<pre>
#include <TFT_eSPI.h> // NOTE: *REQUIRES* TFT_eSPI by Bodmer version 2.3.70 - Attempting to upgrade to newer versions causes this
          //       build to FAIL (even version 2.4.2 FAILS)
</pre>
You can download that specific version of tht TFT_eSPI library from here -
<pre>
          https://github.com/Bodmer/TFT_eSPI/tree/2.3.70
</pre>
NOTE




I purchased (2023-March( an ATS-25X2 (supposedly "WiFi-enabled") radio from Amazon. It came with PE0MGB's 2022-09-17 V.5.3.b firmware running on an ESP32-WROOM-32. It was marketed as a "WiFi-enabled radio". Its WiFi module was hard-coded to the access point "ChinaNet-302" and could not be changed from the front panel. It also did not respond to any prompts over its USB-to-serial port. So I tracked down this firmware and modified it.

This repo contains my mods to the above-mentioned firmware in an effort to better understand it, change its hard-coded WiFi AP setting, and make it at least begin to communicate over the USB-to-serial port about what's going on

This version still has the AP choice hard-coded (I didn't get too far with that part) but at least I started making the device communicate with the USB-to-serial port so you can watch/figure out what the radio is currently listening to


I wanted to publicly archive this version in case anyone else wanted to take advantage of my mods

LIMITATIONS: This version took a shot at deciphering and displaying the currently-tuned frequency and mode at 115200 baud over the USB/emulated serial port. The algorithm displays its best guess, in CSV form, with the following format -

F,14275,M,USB,B,-1000,X,23

where:
      F = Frequency
      M = Mode (USB, LSB, CW, AM, FM)
      B = BFO offset (from -15000 to +15000, in steps of 1000)
      X = "band index" -- this is just a number that the chip/code uses, from 0 to (I belive) 24 or so

My intention was to use this protocol to both display the current radio settings and (eventually, but not implemented yet) control the radio over the USB-to-serial port

I haven't yet gotten the set-frequency commands going. Right now the radio won't respond to anything you send it.

Another note: If the radio does not connect to WiFi it will tie up the radio, considerably, and make the front dial seem unresponsive.  So your best bet is to ENSURE you connect, and STAY CONNECTED to the WiFi access point that is hard-coded into this firmware.

I will look into making this setting user-configurable, but that is likely quite a way off. In the mean time, I might try to lessen the impact of disconnection from WiFi.

SIDE NOTE: When using an Arduino IDE, set the board to "ESP23 Dev Module", and you should be fine.

Cheers!
