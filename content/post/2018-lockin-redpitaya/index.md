---
title: Using the RedPitaya Lock In amplifier
summary: A short and not very clean description of the lock-in module for the RedPitaya
authors:
- hesse
- hoecker
- jendrzejewski

date: 2018-12-10
lastmod: 2021-01-04T17:18:00+01:00
draft: true

tags:
- RedPitaya
- lockin
- tutorial

links:
  - icon_pack: fab
    icon: github
    name: Code
    url: https://github.com/ahesse93/RedPitaya_LockInAmplifier
---

To generate the whole project, open the Vivado TCL console, cd to the
directory where the files are stored and enter
`source RedPitaya_LockInAmplifier.tcl`

A new folder "RedPitaya\_LockInAmplifier" containing all the project
files should be generated, and you should be able to open the block
diagram in Vivado and make changes.

Currently the lock in amplifier on the RedPitaya runs exclusively on the
FPGA - meaning there is no front end, or even C code controlling it. In
order to modify settings the changed parameters have to be written
directly into the FPGA's memory.

Luckily, the RedPitaya has a tool built in to do so: The **monitor**
tool.

In order to use it, one has to connect to the RedPitaya via
SSH: `ssh root@"your ip"`, with "your ip" replaced with your IP
(**129.206.183.98**, presumably), entered in the command line. The
password is **root**.

Enter then `monitor "your address"`, and replace "your  address" with
the address for the setting you want to read out (eg. 0x40000000). The
tool will return the value written to this address *in hexadecimal
format.*

To write a parameter, use `monitor "your address" "your value"`, where
"your value" is the value you want to write *in decimal
format. *Currently all parameters are 32 bit in two's complement, so the
largest value you can write is 2147483647, values larger than that are
probably treated as negative.

Values that you can currently adjust are: Phase, gain at the low pass,
output gain, frequency, low pass frequency. Remember to write down your
settings (if required), as they will be reset after re-loading the FPGA
code (after restarting the RedPitaya, or after an "Update")

A brief description of each will follow:

# Parameters


## Gain at the low pass: 0x41220000

This allows you to amplify the signal you send into the low pass filter,
increasing the precision of the filter. If you set this value too large,
you will get distortion at the low pass, creating harmonics and messing
up the signal. You should set this value as large as possible though, to
get the best performance out of the low pass (eg. the value at which
distortion happens divided by 2)

A sane value might be 50, initially it is set to 1.

## Output gain: 0x41210000

This sets the output gain. Set it as large as you please / until you see
a signal. This does not necessarily degrade your signal, as the lock in
currently works with 32 bit precision internally.

Initially it is set to 1.

## Phase: 0x41200000

Sets the phase between the sine wave outputted on channel 2 and the sine
compared to the input signal. Choose a value that gives you maximum
contrast and the right sign in front of the output signal.

Initially it is set to 0.

## Frequency: 0x41230000

Sets the frequency the lock in is using. Input is 24 bit, leading to a
frequency resolution of \~ 6Hz - so the output frequency should
be $value_{@0x41230000}\ \cdot5.96\ Hz$. Higher frequencies generally
are desirable, as noise often goes with 1/f, but they need to still be
in the system's bandwidth.

Remember to adjust the low pass cutoff frequency after changing the
frequency here (if necessary).

Initially set to 83 -\> 495 Hz.

## Low pass frequency: 0x41240000

This is a kinda tricky one: The filter is an IIR filter, based on Output
= (1-a)\*Input + a\*\[Previous Output\]. a can be calculated
using $a=e^{-\frac{1}{d}}$, where d is the time constant of the low pass
filter **in samples.**

To make this filter efficient, it is downsampled to about 7629 samples /
second, so for a time constant of a second d = 7629.

Another hoop you have to jump through to set this is that this value is
not an integer. After calculating a you need to convert it to binary
(Wolfram Alpha can do that), and take the first 30 bits after the comma
/ point. You then convert these 30 bits back to a decimal number, giving
you a number between 0 and 1073741824. This can be inputted to the FPGA
using the monitor tool.

It is initially set to 7.629 samples -\> 1 kHz / a = 941831214

## Modulation Amplitude: 0x41250000 // not installed on the Red Pitaya right now

Initially set to 65535 = FFFF\_16 = 1V, can be used to scale down the
amplitude of the oscillation

## Good to know

Sometimes it might be necessary to re-load the FPGA code, as the code
has been reset to the factory settings (eg. after a power outage). Do
that by executing `cat /root/lock_in.bit > /dev/cdevcfg` after
connecting to the root account of your Red Pitaya via SSH. Here
/root/lock\_in.bit is the path / name under which I will save the
bitstream code for the FPGA, and /dev/cdevcfg is the folder in which the
FPGA code is stored.

You can also revert this action (in case you want to return to the
factory settings) by
executing `cat /opt/redpitaya/fpga/fpga_X.XX.bit > /dev/xdevcfg`, where
X.XX has to be replaced with the version number of the FPGA code you
want to return to (eg. 0.94)
