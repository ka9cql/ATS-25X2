# ATS-25X2
My mods to the V.5.3b 17.09.2022 PE0MGB SI4735-Radio-ESP32-Touchscreen-Arduino



NOTE: See the source code for this note (and more information about where to get this - and other - files/libraries) -
<pre>
#include <TFT_eSPI.h> // NOTE: *REQUIRES* TFT_eSPI by Bodmer version 2.3.70 - Attempting to upgrade to newer versions causes this
            //       build to FAIL (even version 2.4.2 FAILS)
</pre>
NOTE




I recently (2023-March) purchased an ATS-25X2 (supposedly "WiFi-enabled") ATS-25X2 radio from Amazon. It came with PE0MGB's 2022-09-17 V.5.3.b firmware running on an ESP32-WROOM-32. It was marketed as a "WiFi-enabled radio". Its WiFi module was hard-coded to the access point "ChinaNet-302" and could not be changed from the front panel. It also did not respond to any prompts over its USB-to-serial port. So I tracked down this firmware and modified it.

This repo contains my mods to the above-mentioned firmware in an effort to better understand it, change its hard-coded WiFi AP setting, and make it at least begin to communicate over the USB-to-serial port about what's going on

This version still has the AP choice hard-coded (I didn't get too far with that part) but at least I started making the device communicate with the USB-to-serial port so you can watch/figure out what the radio is currently listening to

I abandoned this project shortly after doing these initial mods, as I began to better understand the limitations of this radio - chiefly, the lack of 10 meter reception. This caused me to abandon the ATS line of radios in favor of the uBITX line - which has both receive and transmit, plus the missing 10 meter capability.

I wanted to publicly archive this version in case anyone else wanted to take advantage of my mods, and also in the rare case that I may want to pick back up where i left off in the future

LIMITATIONS: This version took a shot at deciphering and displaying the currently-tuned frequency and mode. The algorithm displays its best guess, in CSV form, with the following format -

F,14275,M,USB,B,-1000,X,23

where:
      F = Frequency
      M = Mode (USB, LSB, CW, AM, FM)
      B = BFO offset (from -15000 to +15000, in steps of 1000)
      X = "band index" -- this is just a number that the chip/code uses, from 0 to (I belive) 24 or so

My intention was to use this protocol to both display the current radio settings and (eventually, but not implemented yet) control the radio over the USB-to-serial port

I never got that far, as I learned this radio lacked support for the 10 meter US Amateur Radio band
