DECAMUX
=======

BeBoPr++ expansion board for up to 10 axes.

![](http://imageshack.com/a/img904/443/lyiEKz.jpg)

# Introduction

The **DECAMUX** board allows to extend the **BeBoPr++** with another set of 5 axes, for a total of up to 10 axes. A tiny (1.5 x 1.1 inch or 42 x 28 mm) adapter board in combination with some new PRU software allows MachineKit/LinuxCNC to control 10 axes at simultaneously.

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
![](http://imageshack.com/a/img746/7889/f8d8ak.jpg)
*Bottom side, SMD only*

![](http://imageshack.com/a/img902/3377/YdcUG1.jpg)
*Top side, without connectors*

![](http://imageshack.com/a/img746/6573/f6UvU1.jpg)
*Top side, with connectors*

![](http://imageshack.com/a/img911/9549/nnjgt5.jpg)
*Bottom of completed board*

![](http://imageshack.com/a/img673/2575/1gzmfG.jpg)
*An extra cable connects the DECAMUX to the BeBoPr++, the PEPPERs now plug into the DECAMUX*

## The DECAMUX software
The PRU code needed for to used the DECAMUX with MachineKit is available [here](https://github.com/modmaker/machinekit/tree/feature/poc-decamux). This software will be integrated in MachineKit in the near future. An updated pepper driver component and sample configurations are in the repository too.

## How to buy / build

The [DECAMUX board design](https://github.com/modmaker/DECAMUX/blob/master/pcb/DECAMUX_schematics.pdf) and [associated software](https://github.com/modmaker/machinekit/tree/feature/poc-decamux) are available as Open Source. Anyone used to soldering SMD components should be able to assemble a board. L, R and C components are all (large) 0805 parts, the latches are fine pitch but, when using plenty of flux, easy to solder.

See ref [2] in the announcement for quick ordering a set of 3 PCBs at OSH Park.
