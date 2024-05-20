
# DolphinDOS 3

This project [recreates work done on DolphinDOS 3 by SilverDream!](https://e4aws.silverdr.com/projects/dolphindos3/) in KiCad with some adjustments for C128DCR. Go there for a lot of information about DolphinDOS.

The goal was to get rid of 40-wire ribbon cable between daughterboard and IDC to IC adapter and plug the board directly into C128DCR mainboard into U101 (6502 CPU) footprint.

With a ribbon cable extension the same board can be still used with 1571 from C128D or standalone 1571 or installed in 1541/1541-II.

# Project

All the Kicad files are in dolphindos3-kicad/ folder.

Also check dolphindos3-kicad/plots for schematic PDF and gerbers for manufacturing.

## Design changes

- IDC socket and CPU socket swapped around, additional footprint for pins going down to C128DCR U101 socket
- support for 64K ROM (27E512), short/open JP3 to choose which half is used; if you have C128 Kernal switcher then connect JP3 square pad there so that A15 line (pin 1 of ROM) of both C128 Kernal and 1571CR DOS changes simultaneously
- JP3 makes JP1 obsolete you can switch between stock (or JiffyDOS) and DolphinDOS on the fly; JP1 can be used to disable onboard RAM
- support for 32K (62256) and 8K (6264) SRAM chips; for 32K option additionally JP4 and JP5 choose if PIA port B bits 0 and 1 are used to select 8K bank visible in $6000-$7FFF range; this is not supported by any software right now; you can keep those jumpers open

## C128DCR preparation

1. Desolder U101 (6502)
2. Put a socket in that place
3. Put back 6502 and test if the drive still works

# Firmware / ROMs

Firmware is in roms/ folder:

- dd2_kernal_rom.bin - C64 DolphinDOS 2 Kernal, it works with drive's DolphinDOS 3
- sd_dd2_kernal_rom.bin - same, customized by SD!
- kernal-dolphin128.bin - C128 DolphinDOS Kernal, for C128DCR (32K U32 ROM) it has to be combined with C64 Kernal and C64 Basic
- 3dosa_c_27c256_payload.bin - 1541 DolphinDOS 3 ROM
- 1571-dolphin-dos-3.bin - 1571 DolphinDOS 3 ROM, works in C128DCR (1571CR) as well as standalone 1571 or internal 1571 from C128D

# Results

Benchmark results from 64'er speed test show that in C64 mode the internal 1571 drive is 31 times faster on PRG LOAD than a stock 1541.

