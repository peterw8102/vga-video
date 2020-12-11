# vga-video
8Bit VGA Video Card for my Z80 SBC. This repo will initially contain the code for the programmable logic devices and might eventually include some test/demo software for the card eventually.

This video adaptor is designed as a daughter card for [my Z80 SBC](https://easyeda.com/peterw8102/simple-z80) and some understanding of the control signals on that card are useful.

Points to note:
+ The CPU board includes an I/O address decoder where spare lines are taken to the edge connector as the GIST_1-5 lines. This card uses GIST_5
+ The CPU board also includes a simple paged memory mapper mapping any 16KB from a 4MB address space into any of 4 16K slots in the native Z80 16 bit address space. The 8 extended address bits are taken to the expansion connector as BA21-BA14. This card uses these to decode the video memory to the top 16K page in the 4MB space.

## GALS
The design uses a set of GAL programmable devices to provide most of the logic required to drive the card:
+ **LINE_CNT** - 10 bit counter that ticks out each bit in a horizontal scan line, resetting at a count of 800
+ **LINE_DEC** - Decodes values from LINE_CNT in conjunction with VERT_DEC signals to generate a set of control signals
+ **VERT_CNT** - 10 bit counter counting out each scan line from 0-524
+ **VERT_DEC** - Decodes the 10 bit VERT_CNT values to generate vertical control stignals
+ **MEM_DEC** - Very simple logic to interface the CPU to the dual port memory
+ **IO_DEC** - Completely unrelated to video, the card also includes an 8 bit input and an 8 bit input port, this decodes the control lines


