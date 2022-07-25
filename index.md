# Welcome to an HowTO with OpenOCD on TI's K3 SoCs

* TOC
{:toc}

# Introduction

System on Chips (SoCs) are complex one way or other. Gone are the days where you can stare at code
and figure out exactly where your code broke, meh.. at least that would be a bit inefficient use of
your time.

## Basic JTAG concept

[JTAG](https://en.wikipedia.org/wiki/JTAG) debugging tools is essential in the toolkit
of an embedded engineer. And it has been always there for eons.

At the very basic level, JTAG is a scan chain as shown in the following picture from wikipedia

![JTAG Daisy Chaining](https://upload.wikimedia.org/wikipedia/commons/c/c9/Jtag_chain.svg)

There is a clock, and data goes in, and data comes out, and it daisy chains from one device to the next.

However, most of us dont work at the signal level. Instead, we use this to communicate with an internal
hardware block that in turn allows us to talk to actual processors, since that is where the fun stuff is..

For example, when working with TI Processors, the debuggers that people get started with is 
[Code Composer Studio (CCS)](https://en.wikipedia.org/wiki/Code_Composer_Studio) and sometimes, [Lauterbach](https://en.wikipedia.org/wiki/Lauterbach_(company)).

## Code Composer Studio (CCS)
The following image shows how such a communication looks like with CCS. The JTAG debugger you
would probably use in this case might be an [XDS560](https://www.ti.com/tool/TMDSEMU560V2STM-U) or 
on the cheaper end [xds100v2](https://www.ti.com/tool/TMDSEMU110-U)

![Debug Signalling with CCS](img/ccs.drawio.svg)

You can ofcourse find a lot more details in [CCS getting started page](https://software-dl.ti.com/ccs/esd/documents/users_guide/ccs_debug-main.html)

Much of this is ofcourse developed inhouse, inside TI. Ofcourse, there are similar tools from
various SoC manufacturer as well.

## Lauterbach (Trace32)

At an industry level, Lauterbach or Trace32 (as people like to call it), is a much venerated debugger.
So much so that it that some call it the "lamborghini" for debugging. Their offerings are
[varied](https://www.lauterbach.com/frames.html?powerdebugpro.html) with functionality scaling
scaling way up into pretty much fancy features. But then, when you pay the top $$$, you do expect
to get the $$$s worth of features..

Usage model mostly follows a similar sequence of debugger (with so called dongle)+ IDE interfacing
with the jtag signals (in some cases, additional trace signalling) and providing a view to the user
from different perspectives (from Processor, or from debug system etc)

![Debug Signalling with CCS](img/trace32.drawio.svg)

## openOCD

And then, one of the most cost effective option is [openoCD](https://openocd.org/)

This gets a little interesting.
