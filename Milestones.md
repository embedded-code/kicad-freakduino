# Project Milestones #
Most recent at the top

```

```

## Final Prototype Built and Working ##

2013-11-07:  Version 1.2 (r189) is finally built and fully operational, with no further bugs having been found. Yay \o/

See the [project README](README.md) for a photo image of the board.

```

```

## All Systems Go

2013-08-17 (r178): Finally, the first-build board is fully debugged and working 100% OK.

I've learned a whole bunch of little, practical details from this project. Quite happy with the results.

Later: (r181) I've done a dozen or so more improvements around the board, mostly to the ground planes. Gosh. I don't think I've ever spent so long, futzing around with a PCB design. With this one, I seemed to endlessly find things in need of improvement. I guess I'm nervous because I already messed up twice and it cost me. Never the less, I'm pretty happy with how things stand at (r181). So, I'll probably order the FINAL (dag-gone-it! :-P) batch of prototype proofing boards, shortly.

## <b>Revision r181 - v1.2</b>

### 3D View
<img src='images/pcb-3d-r181.png' />

### PCB Layout
<img src='images/pcb-layout-r181.png' />

```

```

## First Physical Build

2013-08-13: First physical test board (<a href='https://code.google.com/p/kicad-freakduino/source/detail?r=116'>r116</a>) -- patched to work around errors ...

<img src='images/first-build-r116.png' />

### Several Errors Found

<blockquote>Random Reminder: <i>I'm just an amateur home hobbyist, doing/copying this for fun and learning.</i></blockquote>

I finally got to (hand) build the first prototype (semi-clone/copy, that is) version 1.0 (<a href='https://code.google.com/p/kicad-freakduino/source/detail?r=116'>r116</a>).  Here it is ...

Alas, more errors were discovered ...

 * The slide switch pin numbering was reversed, thus reversing its function, according to silk labels and original Freakduino.
 * Due to an error in the bill of materials (BOM) spreadsheet, I had ordered the wrong 3.3V regulator, having the more common GOI pin order, instead of the prescribed IGO version.  I rigged what I had to work by standing it up and installing a wire link -- until I get the right parts in.
 * Due to another error in the BOM, I had ordered the wrong size 100uF capacitor, C3. (I had an 8mm dia. but needed a 6.3mm dia.)
 * The buck boost regulator wasn't producing the goods. The problem turned out to be that I used too small an inductor. I guess the core on the tiny 0603 part was saturating. A larger inductor (salvaged from an old hard drive and adhered to the board with shoe repair glue :-P) got things working well. Later, some NR4018 inductors were purchased and tested all good.  (That tiny TPS61222 chip can supply 500mA! Amazing.)
 * The RF chip crystal pads were mirrored. (Didn't see the word, "bottom" in the datasheet.)
 * The GTL2003 DREF/GREF pins were wired wrong, causing the chip to cook. (This time, I hadn't read the datasheet well enough, at all. <i>sigh</i>) I also realised that, since the GTL2003 is open-drain output and is connected to an SPI bus without need for external pull-ups, the ISP programming jumper JP2 is not strictly needed. But I left it in place, just in case.
 * 

As at version v1.2 (r178) the project BOM files and PCB design have been updated and corrected, according to the above. Quite a lot of general tidying was also done.

The RF section has now been tested working. But proper range tests have not yet been conducted.

<b>Frequency</b>: The original Freakduinos appear to be using an 8pF (16MHz) crystal, with 12pF capacitors. I measured the oscillator frequency at 16.9997MHz -- 500Hz lower than my 12pF crystal and caps. This represents a 31ppm difference (if you can trust my math) which seems like it should be too much. But the two radios do communicate OK. The radio chip also has internal trimmer capacitors, which can be adjusted digitally. Chibi does not appear to provide API access to this feature. I might add it.

As an experiment, I pushed the difference out to 5,000Hz (10x before) and confirmed that radio comms failed, as expected. Interesting, though.

It's hard to know exactly what frequency the 16MHz oscillator is really running at, since the test probe loads the circuit. However, I would suspect that the test probe loading reduces the frequency a little. Therefore, it appears to me more likely that Akiba's choice of an 8pF crystal is the way to go. So, I update update the BOM to an 8pF version and order some for myself. (They're not cheap here, at over $7 each!)

That said, my 8-digit counter claims to be good to 2.7GHz. So I should really use the RF chip's feature to turn on a test carrier and measure the final output. Perhaps tomorrow.

<b>Range tests not withstanding, r178 <i>might</i> be the final v1.x production-proof.</b>

Later the same day -- after some excitement initially with non-connecting antennas -- range checks and signal RSSI reports are all good. Excellent. Whew!

```

```

## PCBs Ordered for KiCAD-Freakduino v1.0 (r116)

<img src='images/pcb-order.png' align='right'>Enough tinkering already! Time to order the first 10 prototype PCBs and get cracking.

I actually ordered boards for r101. But later found errors, which have been corrected in r116. So the r101 boards are now pretty, blue and gold tea coasters -- before they even get out of production. *sigh*

I've ordered 10x PCBs (minimum quantity) and all the parts to build two boards, with the usual bulk left-over resistors, capacitors purchased for reasons of economy and use in later projects.

<blockquote>NOTE:  Enough parts to build just two (2) of these boards has cost more than USD$200, including the PCBs. So don't bother building, unless you really want the educational experience, as I did. Instead, I recommend you simply buy genuine units from the <a href='http://freaklabsstore.com/'>freaklabsstore.com</a> at just USD$36 ea. (2013-07-23) fully built and tested.</blockquote>

My goal ultimately is not to build Arduino compatible boards, but small, bare bones boards based on what I've learned here, for use in sensor networks and for wireless remote control. I'd also like to play about with low power Bluetooth™ and Wi-Fi, as experience and understanding increases. But who knows.

### PCB Layout Overview v1.0 (r=116)

#### A 3D View v1.0 (r116)

<img src='images/pcb-3d-r116.png' />

#### CAD View v1.0 (r116)

<img src='images/pcb-layout-r116.png' />

````

```

### Notes for r116 Milestone

Some components and their related layout design work differ from the authentic Freakduino v2.1a. This was driven in the first instance from lack of availability of certain parts, at the time. A source was finally located in China and parts ordered. But I decided to stick with the more readily available versions anyway.

So, the final routing solution ended up significantly different to Akiba's original design, because it just seemed easier to route using my own brain, than trying to copy. (The different battery holder mounting hole position(s) and the two substituted chips with supporting parts mandated changes, anyway.) However, I was careful to leave the user interaction devices -- antenna and power connectors, dip switches, jumpers and LEDs -- in very similar to original locations, so that the original documentation may better apply to this design.

Some minor layout errors were found with regard to positioning of some 0u1 decoupling capacitors (C18, C20, C21 from memory) in the authentic Freakduino. Nothing serious, just some swapped positions, basically. In any case, these were "corrected" in this KiCAD rendition.
