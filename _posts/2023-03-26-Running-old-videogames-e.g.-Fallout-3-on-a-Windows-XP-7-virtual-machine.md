---
layout: post
title: "Running old 3d games (e.g. Fallout 3) on a Windows XP/7 virtual machine"
tags: [3d,gaming,legacy,retrocomputing,virtualization,vmware,vfio,virtualbox,windows]
last_modified_at: 0000-00-00 00:00:00
---

A well-known problem in retrogaming is to be able to run games that are compatible only with old Windows systems, like Windows XP/7, and that require 3d acceleration.

In this article I'll explore how to solve this problem, and describe my experience with how the most common virtualization software handles this requirement.

This article also helps when testing cross-platform game development, which can be a tedious task, since transferring compiled games across machines is an annoying process.

Content:

- [First Header](#first-header)

## The problem, and the invalid solutions

Running old 3d games is an interesting problem. Games of the 2000 decade (Fallout 3, Grand Theft Auto 3, ...) are resource-intensive enough that they can't be emulated by a pure-software emulation, but old enough - therefore, with an O/S unsupported by modern drivers - that can't be run by passing a GPU through.

The following solutions are thefore invalid:

- PCem: the most powerful card [supported](https://pcem-emulator.co.uk/status.html), the 3DFX Voodoo 2, doesn't support Windows XP/Direct3D; even if a virtual 3d card were supported, it would be too demanding to be emulated by a CPU (PCem does not use 3d hardware acceleration by design)
- QEMU+VFIO: this QEMU configuration doesn't support legacy BIOS, which is required by Windows XP (see [here](https://www.reddit.com/r/VFIO/comments/u3cuup/is_it_possible_to_boot_a_vm_in_legacy_bios_mode)); even if it worked, it'd require a very old GPU to be plugged to the PC (since modern GPU drivers don't support Windows XP)
- VirtualBox <=6.1: VirtualBox has always had very poor 3d support; I've never been able to make it work successfully
- VirtualBox >=7.0: Doesn't support Windows XP; even if it did, its 3d support is extremely broken (crash on drivers installation is a recognized bug, but even after installation, I got black boxes etc.)

The only valid solution is VMWare, which, fortunately works.

## VMWare, setup and gotchas

VMWare (Player and Workstation share the same engine, so I'll use the "Vmware" term to refer to any) has a very advanced 3d support; as of Mar/2023, the latest versions support (), in the guest (among the other guest O/Ss) Windows XP, and many DirectX/OpenGL versions.

The 3d support is enabled by default (and the guest tools are also automatically installed), so there's nothing to do in the guest; the most important thing is be sure that the host has all the required libraries installed (see [VMWare help](https://docs.vmware.com/en/VMware-Workstation-Pro/17/com.vmware.ws.using.doc/GUID-EA588485-718A-4FD8-81F5-B6E1F04C5788.html); the same applies to VMWare Workstation Player, which doesn't have any significant difference in this context).

On Linux with AMD GPU setups, on needs to make sure that the AMDVLK Vulkan drivers are use (to be cover all cases, set the `AMD_VULKAN_ICD` environment variable to `AMDVLK`); the AMDVLK packages can be downloaded from the [GitHub repository](https://github.com/GPUOpen-Drivers/AMDVLK/releases).

The most important thing to keep in mind is that while VMWare's engine is very advanced, it's also very fragile (I suspect buggy). There are a variety of factors, seemingly unrelated to the 3d acceleration, that cause guest freezing for several seconds, while the CPU on the host goes to 100%.

There are a few factors that I've found causes this:

- setting more than CPU core on the guest, even if the host system has plenty of cores
- losing focus from the guest VMWare window (experienced on Linux)
- switching to full screen (experienced on Windows)

Generally speaking, I advise to set the guest settings to the minimum working value (e.g. reduce the VRAM to the amount required by the game, and so on), and to switch to full screen or other host programs as little as possible.

Some games may still require tweaks in order to work (see next section), but they won't be due to using an unsupported version of Windows, which is often a critical problem.

VMware also has very sketchy resolution handling. Since one needs to use a relatively low resolution, they'll need to enable guest display stretching when on full screen (which is not a default behavior), however:

- stretching the screen has a very poor result, unless one uses an integer fraction of the fully covered dimenstion (for example on my monitor, which has a 3440x1440 resolution, I use 1270x720, since 720 is exactly half of 1440);
- sometimes the stretch is not applied; in such cases, turn off and on again the full screen mode.

## Fallout 3

Fallout 3 is a game that causes considerable headaches when run on an operating system other than Windows XP, often, not being able to run at all. Even on Windows XP, it also had a breaking issue with integrated GPUs (iGPUs).

Windows XP on VMware fits Fallout 3 fine, but one needs to workaround the iGPU problem (VMWare probably presents the virtual card as such); an easy workaround can be downloaded from [here](https://www.nexusmods.com/fallout3/mods/20371) or [here](https://www.mediafire.com/file/idum0obp1zkfwu9/Win_7_and_8_patch-20371-1-0.iso).

During my testing (a couple of hours of gameplay), I've never experienced crashes while playing.

## Performance considerations

On a system composed of:

- AMD Ryzen 7950x with 280mm water cooler,
- DDR5 6000 CL 30,
- Radeon RX 6600 XT,
- Linux,

Fallout 3 ran at solid 60/70 FPS, while using approximately 40% of the host GPU; the host CPU, however, was consistently at 80% utilization.

The bottleneck is likely on the CPU/RAM side; this makes sense, since presumably, a lot of overhead is constituted by translating the calls from the guest APIs (DirectX/Windows) to the host (in this case, Vulkan/Linux), and transferring data to/from the phsyical and the virtual GPUs.
