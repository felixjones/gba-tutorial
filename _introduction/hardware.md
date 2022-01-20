---
layout: post
title: "Hardware"
ordering: 2
---

As said in the previous topic, the GBA has a completely different architecture to the DMG/CGB.

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

This is actually super important for GBA stuff. The ARM7TDMI has fixed-length instructions. ARM instructions are 32-bit, thumb instructions are 16-bit.

The GBA is a 32-bit console, it will boot up reading 32-bit instructions to execute on its 32-bit CPU. But the bus to the cartridge is 16-bit! Which means all 32-bit reads will take two reads. That's not good for performance\*. Also: 32-bits is a lot of bits taking up a lot of space, and the ROM chips on these cartridges cost money.

The smaller 16-bit thumb instructions can be read from the cartridge in 1, the instructions are also much more dense in terms of bit storage, which (in theory) means smaller games, which means smaller ROM chips, so money saved.

> Trivia: There is a reason why 16-bit thumb is so ideal for cheap cartridges on a 16-bit bus, and that's because ARM originally designed thumb with Nintendo and their cartridge consoles in mind. The ARM7TDMI itself (and the thumb instruction set) was published in 1994, some 7 years before the GBA's release date!
