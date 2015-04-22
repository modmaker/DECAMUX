DECAMUX
=======
Last changed: 2015-04-22 - Updated FAQ.


**BeBoPr++ expansion board for up to 10 axes.**

|![](http://imageshack.com/a/img673/2575/1gzmfG.jpg)|
|:-:|
|*DECAMUX with flatcable for connection to BeBoPr++*|

## Introduction

The **DECAMUX** board **doubles the number of outputs** on the **BeBoPr++**'s extension connector. Instead of the single (**J5**) expansion connector, two of these connectors are created, for **up to 10 axes**, **20 digital outputs**, or **a combination** of these (for 3 axes and 4 PWM outputs, see the [**XTRUDR**](https://github.com/modmaker/XTRUDR)). 

The tiny 1.7 x 1.1 inches (42 x 29 mm) adapter board in combination with some new PRU software allows MachineKit/LinuxCNC to control all signals simultaneously. The board has 3 connectors, one connects to the BeBoPr, the other two connect to the expansion boards.

## Announcement
The board was announced on the MachineKit mailing list:

	Hi All,

	Since the release of the BeBoPr++ I've been asked a couple of times
	whether the BeBoPr can control more than the usual 4 or 5 axes. The
	answer has often been: "Yes, in theory. You're only limited by what
	LinuxCNC/MachineKit can control". Other boards, like the CRAMPS or
	Replicape, offer extension-boards to add more axes. But these solutions
	claim more of the BeagleBone's scarce I/O pins. The amount of available
	I/O signals on P8 and P9 is a severely limiting factor. This makes it
	hard to add axes without sacrificing other functionality. There should
	be a better solution...!
	
	During the last couple of weeks I've worked on some hardware and
	software extensions that allows a single BeBoPr++ to control 10 stepper
	motors with two PEPPER boards. In theory it should be possible to extend
	this to even more (15, 20, ...) axes, if only the software were capable
	of handling it. Currently LinuxCNC/MachineKit seems (software-wise?)
	limited to 9 axes.
	
	How is it done? Normally a single PEPPER [3] stepper module connects to
	the J5 expansion connector on the BeBoPr via a 16-wire flatcable. This
	cable carries the signals for (only) 5 axes and some control (as
	documented in the BeBoPr++ manual [1]). Because I've been programming
	the PRUSS from the very beginning, I knew it was capable of doing some
	extra work. So I've modified Charles' PRU code to multiplex two sets of
	5 axes over that single cable, and built a small splitter board to
	de-multiplex those signals again. This splitter board is called the
	DECAMUX. It's now "Open Source Hardware" and available from OSH Park
	[2]. The DECAMUX connects to the BeBoPr on one side, and to two
	(identical) PEPPER boards on the other side.
	
	Since I have no hardware (machine, robot, anything) that does something
	useful with this many axes, I'm looking for volunteers. If you have a
	'many-axes' application, are interested and feel adventurous, contact me
	to see if we can do something with your application. I've got free
	(assembled) DECAMUX boards for the first two or three projects
	demonstrating 6 axes or more!
	
	Cheers,
	-- Bas
	
	[1]
	https://github.com/modmaker/BeBoPr-plus-plus/blob/master/BeBoPr%2B%2B%20User%20Manual.pdf
	[2] https://oshpark.com/shared_projects/Nn0ndOrm
	[3] https://github.com/modmaker/BeBoPr-plus-plus/wiki/PEPPER-Intro

Read the full DECAMUX thread here: https://groups.google.com/forum/#!topic/machinekit/0aYZ0jUaGkY.

## The DECAMUX hardware
|![](http://imageshack.com/a/img902/3377/YdcUG1.jpg)|
|:-:|
|*Bare board*|

|![](http://imageshack.com/a/img746/7889/f8d8ak.jpg)|
|:-:|
|*Bottom side with all SMD components mounted*|

|![](http://imageshack.com/a/img746/6573/f6UvU1.jpg)|![](http://imageshack.com/a/img911/9549/nnjgt5.jpg)|
|:-:|:-:|
|*After mounting connectors, Top side*|*Bottom side*|


|![](http://imageshack.com/a/img904/443/lyiEKz.jpg)|
|:-:|
|*With cable to connect to the BeBoPr++: two expansion connectors available*|

## The DECAMUX software
The PRU code needed for to used the DECAMUX with MachineKit is available [here](https://github.com/modmaker/machinekit/tree/feature/poc-decamux). This software will be integrated in MachineKit in the near future. An updated pepper driver component and sample configurations are in the repository too.

## How to buy / build

![](http://www.oshwa.org/wp-content/uploads/2014/03/oshw-logo-100-px.png)

The [DECAMUX board design](https://github.com/modmaker/DECAMUX/blob/master/pcb/DECAMUX_schematics.pdf) and [associated software](https://github.com/modmaker/machinekit/tree/feature/poc-decamux) are available as **Open Source Hardware**. Anyone used to soldering SMD components should be able to assemble this board. L, R and C components are all (large) 0805 parts, the latches are fine pitch but, when using plenty of flux, easy to solder.

The PCB design is open hardware and available as shared project at **OSH Park**. A set of 3 PCBs can be [ordered directly from OSH Park](https://oshpark.com/shared_projects/Nn0ndOrm) for less than $10 including shipping. Total BOM cost is around EUR 8-10, or $10-$15 for the complete board including cable.

## FAQ
**Q1**: Can I use the DECAMUX together with the plug-in stepper modules?
**A1**: No. The DECAMUX connects to the connector for off-board stepper drivers and uses the same signals as the plug-in stepper modules. Thus it's physically not possible to combine both.

**Q2**: Is the pinout of the output connectors on the DECAMUX different from J5 on the BeBoPr++?
**A2**: No. The signals are the same, although the voltage levels differ (see next question).

**Q3**: I'm using plug-in stepper modules, can I expand my system and continue to use these modules?
**A3**: Yes. For this purpose the [TAKE-5](https://github.com/modmaker/TAKE-5) expansion board was made. It can hold all four modules plus one extra, for a total of five axes.

**Q4**: I am currently using brand 'XYZZY' stepper drivers with the BeBoPr. I would like to add more axes, can I use the DECAMUX?
**A4**: Probably. You have to check that your drivers will work with 3.3 Volt signal levels on the inputs. The BeBoPr uses 5 Volt CMOS levels while the DECAMUX generates lower, 3.3 Volt CMOS levels.

**Q5**: Can I cascade multiple DECAMUXes to increase the number of outputs further?
**A5**: Not yet, with the current DECAMUX and software.

**Q6**: What software can I use with the DECAMUX?
**A6**: The [BeBoPr software](https://github.com/modmaker/BeBoPr) generates step signals for only four or five axes. To work with more axes, [MachineKit](http://www.machinekit.io/) with DECAMUX support is needed (see Q7).

**Q7**: Will the [modified machinekit repository](https://github.com/modmaker/machinekit) with code for the DECAMUX be part of the official code?
**A7**: Yes, soon I hope.

**Q8**: Will the DECAMUX work with the previous generation BeBoPr and BeBoPr+ boards?
**A8**: Not without modifying the BeBoprm but in theory it could be made to work.

**Q9**: I don't want to order 3 boards because I only need one.
**A9**: Post a message on the MachineKit list, or send me a mail and I might have a spare for sale.

**Q10**: I'm only having basic soldering skills. The latch on the DECAMUX has 0.65 mm pitch leads. Help!
**A10**: I'm looking into producing an assembled version. Drop me a mail if you're interested.

**Q11**: What are the jumper settings on the BeBoPr++ when I want to use the DECAMUX?
**A11**: Both JP3 and JP4 on the bootom side of the BeBoPr++ should be closed.

**Q12**: Do I need a special device tree overlay for the DECAMUX?
**A12**: Yes, you need the cape-bebopr-pp overlay instead of the default cape-bebopr-brdg. If you disable the default overlay in uEnv.txt, the proper one will be loaded by the Axis startup script.
