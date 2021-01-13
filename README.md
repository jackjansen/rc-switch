# rc-switch
[![arduino-library-badge](https://www.ardu-badge.com/badge/rc-switch.svg?)](https://www.ardu-badge.com/rc-switch)
[![Build Status](https://travis-ci.org/sui77/rc-switch.svg?branch=master)](https://travis-ci.org/sui77/rc-switch)

Use your Arduino or [Raspberry Pi](https://github.com/r10r/rcswitch-pi) to operate remote radio controlled devices

## Download
https://github.com/sui77/rc-switch/releases/latest

rc-switch is also listed in the arduino library manager.

## Wiki
https://github.com/sui77/rc-switch/wiki

## Info
### Send RC codes

Use your Arduino or Raspberry Pi to operate remote radio controlled devices.
This will most likely work with all popular low cost power outlet sockets. If
yours doesn't work, you might need to adjust the pulse length.

All you need is a Arduino or Raspberry Pi, a 315/433MHz AM transmitter and one
or more devices with one of the supported chipsets:

 - SC5262 / SC5272
 - HX2262 / HX2272
 - PT2262 / PT2272
 - EV1527 / RT1527 / FP1527 / HS1527 
 - Intertechno outlets
 - HT6P20X

### Receive and decode RC codes

Find out what codes your remote is sending. Use your remote to control your
Arduino.

All you need is an Arduino, a 315/433MHz AM receiver (altough there is no
instruction yet, yes it is possible to hack an existing device) and a remote
hand set.

For the Raspberry Pi, clone the https://github.com/ninjablocks/433Utils project to
compile a sniffer tool and transmission commands.

## Changes in this fork 

This fork is jackjansen/rc-switch. It adds support for the ELRO FA500 Flamingo series.

The remote (FA500R) sends multiple codes on every button press. Stock rc-switch
can decode the last 2 codes, but unfortunately these are _not_ the codes that the
switches (FA500S) react to: these react to the first code.

This fork add support for that style of code.

Information comes from:

- <https://gist.github.com/probonopd/331674026839b96cd8d7> had the basics of the
  protocol (sync 1 high 15 low, 28 bits of "usual" 1+3/3+1 ).
- <https://forum.arduino.cc/index.php?topic=201771.0> is the same info in different
  form. Also notices that successive presses of the same button sends 4 different
  codes. The 4 codes are _completely_ different. But: this thread has a reference to the next
  two sites.
- <https://forum.fhem.de/index.php/topic,36399.60.html> is about the Home Easy HE800S
  but apparently these use the same  code. Turns out the switches indeed send a 
  rolling code sequence number (0-3), and the whole packet is encrypted. 
- <https://github.com/windkh/flamingoswitch> has an implementation of the encrypt
  and decrypt routines. Not added here, because the rc-switch code structure
  does not make it easy.
