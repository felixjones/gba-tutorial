---
layout: post
title: "Architecture"
ordering: 2
---

The GBA has a completely different machine architecture to the DMG/CGB.

# The architecture

The GBA was marketed as having a powerful 32-bit **RISC** processor. What does RISC mean? It stands for Reduce Instruction Set Computer. What does that mean? These days: not a lot.

## ARMv4t / ARM7TDMI

The actual processor architecture used in the GBA is the ARM7TDMI. Supposedly the 7th generation of ARM's architecture (hence ARM7). Who is ARM? Advanced RISC Machines.

What does TDMI stand for? Well that stands for:
* 16-bit **T**humb instruction set support
* The letter **D**
* Hardware **M**ultiplication support
* The letter **I**

The primary instruction set for ARM7 is ARMv4 (the forth version of the ARM instruction set!), but because we have support for Thumb instructions the complete instruction set is ARMv4t. The naming convention is a little confusing.

From here on these two instruction sets will be stylised as: thumb and ARM.

> Theory trivia: The reason Nintendo used "RISC processor" in their marketing and not "ARM processor" could be because they didn't have a license to use ARM's trademark.

### Instruction sets

This is actually super important for GBA stuff. The ARMv4t instruction set uses fixed-length instructions. ARM instructions are 32-bit, thumb instructions are 16-bit.

The GBA is a 32-bit console, it will boot up reading 32-bit instructions to execute on its 32-bit CPU. But the bus to the cartridge is 16-bit! Which means all 32-bit reads will take two reads. That's not good for performance (maybe<sup>1</sup>). Also: 32-bits is a lot of bits taking up a lot of space, and the ROM chips on these cartridges cost money.

The smaller 16-bit thumb instructions can be read across the cartridge's 16-bit bus in 1 read, the instructions are also much more dense in terms of bit storage, which (in theory) means smaller games, which means smaller ROM chips, so money saved.

> Trivia: There is a reason why 16-bit thumb is so ideal for cheap cartridges on a 16-bit bus, and that's because ARM originally designed thumb with Nintendo and their cartridge consoles in mind. The ARM7TDMI itself (and the thumb instruction set) was published in 1994, some 7 years before the GBA's release date!

### Clock Speed

The CPU runs at 2^24 cycles-per-second, which is 16.777216 megahertz (MHz). Some instructions take multiple cycles to execute, and some memory accesses take multiple cycles to complete.

## Random Access Memories

But first: a bit about notation.

|IEC name|Traditional name|Quantity  |IEC symbol|LD symbol|
|--------|----------------|----------|----------|---------|
|Byte    |Byte            |8 bits    |B         |-        |
|Kibibyte|Kilobyte        |1024 Bytes|KiB       |K        |
|Mebibyte|Megabyte        |1024 KiB  |MiB       |M        |

When required, we'll use the 1998 IEC names and symbols as they avoid ambiguity. The LD symbols are used in linker scripts, which will be important later.

## Cache?

GBA has no cache.

### Internal RAM

But isn't all the RAM internal? Well yes, but this is "internal" from the perspective of the CPU.

The internal RAM is on the same physical package as the CPU.

#### 32KiB Internal Work RAM

IWRAM for short. This is fast RAM on a 32-bit bus: perfect for fast, optimised ARM instructions and stack memory.

#### 96KiB Video RAM

VRAM for short. This is where all the background and sprite graphics will live. You can only access this memory in units of 16-bits, so to write a single byte you have to first read 16-bits, modify the byte you're interested in, then write back 16-bits. Watch out for that.

#### 1KiB Palette RAM

PRAM? CRAM for colour RAM? There's no general short term for this RAM, so we'll just call it Palette RAM. This holds two palettes of 256 colours (Colours are 16-bit). One palette is used for background graphics, the other is used for sprite graphics.

> Trivia: Yes the author is British. I will use the spelling "colour" for any written text, and "color" for any code. Did you notice how I spelled "optimised" above?

#### 1KiB Object Attribute Memory

OAM for short. This stores everything related to setting up hardware sprites for display.

### External RAM

EWRAM for short. External from the CPU package, this RAM is still on the motherboard in its own little chip.

256KiB on a 16-bit bus. 32-bit accesses are automatically converted to two 16-bit access. Traditionally this is where the heap is placed for big allocations (because we have soooo much space with 256KiB). This is slower than IWRAM, and being 16-bits makes this more ideal for thumb instructions, rather than ARM instructions.

### Save RAM

SRAM for short. This isn't actually part of the console, it resides in the game pak (the cartridge). This is only available on cartridges with a RAM chip on board. 8-bit accesses only, and the hardware does nothing to help if you want to access 16 or 32 bits.

The 8-bit accesses makes this kind of slow. Intended for saving data, like a save file or something.

Maxes out at 64KiB, but 32KiB is what you usually find out in the wild.

## Game Paks

AKA: the cartridge, and the ROM. The maximum addressable size is 32MiB, however 64MiB cartridges do exist (those weird GBA video cartridges are such examples), and these achieve greater capacity through bank switching.

Some cartridges have additional hardware on them, such as a real-time clock, a vibration motor, a tilt sensor, a freaking analogue TV tuner, and a crazy card-scanning accessory.

### Game Pak Prefetch

This is a weird bit of hardware that is designed to try and speed up executing code from the Game Pak ROM. After fetching an instruction from ROM, whenever the CPU is not accessing the bus the prefetcher will further read up to an additional 8 16-bit values from the ROM, and store them internally. If the next access the CPU makes is within the area of ROM currently in the prefetch buffer then it will be read immediately (0 wait-cycles).

In practical terms, this usually ends up with ROM thumb instructions in the prefetch buffer (because the next CPU read is usually the next instruction in ROM).

This hardware feature requires explicitly enabling, and it's usually worth doing if you're executing anything from ROM.

***

<sup>1</sup> Theoretically, if you're able to do something in ARM with 50% less instructions than in thumb, then executing ARM across 16-bit bus might not be such a bad performance hit. However, not all instructions are identical, so it is quite unlikely you'd naturally stumble across a scenario where this makes sense.
