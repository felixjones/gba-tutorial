---
layout: post
title: "Toolchain"
ordering: 1
---

# gba-toolchain

This setup tutorial will cover compiling a GBA ROM with the [gba-toolchain](https://github.com/felixjones/gba-toolchain). What is the gba-toolchain? Well, it's a CMake-based toolchain written by yours truly.

## CMake

Like it or not, CMake is the industry standard for modern C/C++ development (as of 2022, at least), and I promised that this tutorial will cover GBA development in the modern age.

CMake has a pretty handy mechanism for cross-compiling called "CMake toolchains". [gba-toolchain](https://github.com/felixjones/gba-toolchain) is a CMake toolchain, but one that sets up everything you need for GBA development, including tools and libraries.

gba-toolchain requires CMake 3.20, so go ahead and [download CMake](https://cmake.org/download) if you're following along.

## Visual Studio Code

Modern IDEs tend to have good support for CMake based projects. VSCode is one of them (via the CMake plugin). Like CMake, it's cross-platform.

[Download VSCode here](https://code.visualstudio.com/). Oh and important note: **VSCode is not Visual Studio**. Cross-compiled CMake projects can work with Visual Studio, but it's both Windows-only and isn't a common use case of Visual Studio (so its support can be buggy).

Once you've got VSCode installed, click the extensions button so we can download everything needed for C/C++ devel  opment.

<img src="assets/vscode-0.png" alt="Start screen of VSCode with an arrowing pointing at the extensions button"/>

### C/C++ Development Extension

This is a Microsoft extension for VSCode that adds language support for C/C++ to VSCode, including debugging!

This also comes with CMake support (handy!).

<img src="assets/vscode-1.png" alt="Start screen of VSCode with an arrowing pointing at the extensions button"/>

Searching "C++" in the extensions window should get you to the Microsoft C/C++ extension.

Click Install.

## gba-toolchain CMake toolchain

You can either download the repository from [github.com/felixjones/gba-toolchain](https://github.com/felixjones/gba-toolchain), or you can just download the toolchain script from [github.com/felixjones/gba-toolchain/3.0/arm-gba-toolchain.cmake](https://raw.githubusercontent.com/felixjones/gba-toolchain/3.0/arm-gba-toolchain.cmake).

Extract the repo (or save the script) to a location that you can reference later.

# devkitARM

devkitARM is an alternative toolchain to gba-toolchain (or gba-toolchain is an alternative to devkitARM?). It's the current de-facto toolchain (and environment, on Windows) for building GBA programs, so many tutorials out there will reference devkitARM (or devkitPro, the organisation name).

devkitARM is a bit long in the tooth: GBA updates are sparodic, it uses its own fork of GCC and binutils, for some reason, and it is Makefile based by default (also, on Windows it requires a binary installer and MSys2).

devkitARM is fine, but you won't get the modern comforts that gba-toolchain provides.
