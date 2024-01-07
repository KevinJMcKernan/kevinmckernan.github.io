---
layout: post
title:  "8-Bit Computer - EEPROM Programming Part I"
date:   2023-10-15 14:00:10 -0400
categories: webpage
---

# 8-Bit Computer - EEPROM Programmer

Continuing the build out of Ben Eater's super cool 8 bit computer kit.
[8bit](https://eater.net/8bit/)

Constructed the EEPROM programmer. With prograbably my worst wiring to date.  

EEPROM Programmer
![programmer](/assets/images/programmer.jpg)

Ran into difficulties programming the AT28C16 chip. Long story short, swapped it with one of the other 2 available. And it worked! Bad chip.

Unfortunately the AT28C16 is discontinued and no longer available on Jamco or Mouser. Luckily the AT28C64 is! And has a 'mostly' similar pin layout. 
Frustrated, I pulled out a TL66II+ programmer instead of updating the bread board programmer. 

Fancy Programmer
![fancy_programmer](/assets/images/eeprom_programmer.jpg)

Steps Followed:
1. Installed [minipro](https://gitlab.com/DavidGriffith/minipro/)
2. Searched for the chip with cmd line: $ minipro -L AT28C64B 
3. Write some hex as a binary file. 

	import binascii
	test = [0x81, 0xcf, 0x92, 0x86, 0xcc, 0xa4, 0xa0, 0x8f, 0x80, 0x84, 0x88, 0xe0, 0xb1, 0xc2, 0xb0, 0xb8 ]

	with open('file.bin', 'wb') as bin_file:
		for x in test:
			print(bytes((x,)))
			bin_file.write(bytes((x,)))
4. View file with $ xxd -b file.bin
5. Program the chip with $ minipro -p AT28C64B -w file.bin -s
6. Verify by reading the chip to a new file with $ minipro -p AT28C64B -r test.bin -s

Side Note: My brain must have been in dumb mode. I checked amazon. . . AT28C16's are available for a couple bucks. 

















