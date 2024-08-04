---
title: GPU compatibility matrix
permalink: /GPU_compatibility_matrix/
---

This table gathers test results about various hardware and software
configurations,
<span style="background-color: green !important; color: white !important; padding: .25em .5em;">passed</span>
means nothing wrong is noticed and frame rate is at least <u>60 fps</u>
on common scene,
<span style="background-color: lightgreen !important; color: green !important; padding: .25em .5em;">playable</span>
means at least <u>30 fps</u>.

All those tests were driven by Unvanquished developers or under
Unvanquished developer supervision.

See [below](#Comprehensive_analysis "wikilink") for analysis, specific
definitions and meanings.



<hr/>



## Comprehensive analysis

Minimal configuration for the Unvanquished game is OpenGL 3.2.
Unvanquished can run on OpenGL 2.1 hardware but this would not be
playable because because we use models with more than 41 bones and
OpenGL 2.1 cards can't accelerate them enough. It will run but it will
be slow.

Decent performance (given advanced graphical effects are disabled)
starts with AMD/ATI TeraScale GPU, Intel HD Graphics (HD 4000), Nvidia
Tesla-based GPUs. Though, it is strongly discouraged to buy GT218-based
GPU like the Geforce 210 one as the proprietary driver for them is known
to be buggy, requiring the engine to implement workarounds for it (save
a game developer, do not buy this GPU!).

To play at 4K resolutions, high-end AMD GCN/RDNA is recommended: AMD R9
390X from 2015 can handle `ultra` preset with 4K resolution at 144Hz.
AMD R7 Embedded in R series APU can handle 2K resolution with `medium`
preset (no realtime light and relief mapping disabled) as well as Intel
UHD.

Minimal configuration to run the Dæmon engine is OpenGL 2.1 with
`ARB_half_float_vertex` and `ARB_framebuffer_object`
(`EXT_framebuffer_object` is not enough). It includes ATI/AMD GPU
starting with R300 (Radeon X300), Intel GPU starting with GMA965 (X3100)
on Linux and macOS, HD Graphics on Windows, Nvidia starting with Curie
(NV40, Geforce 6xxx). Wikipedia says the GMA965 Windows driver only
supports OpenGL 1.5 and then would not reach the requirements for
running Unvanquished on this platform. If you plan to make a game using
Damon engine supporting those older cards, make sure your animated
models don't have more than 41 bones.

## How to contribute

This matrix is generated from a cell sheet. Do not edit it by hand,
Please ask `illwieckz` for access to the cell sheet.

Please sort your contributions by brand (ATI/AMD, Intel, Nvidia, Via…)
then by launch date (from newer to older).

The table also documents who may be able to reproduce a special
configuration, please put your nick name and tell how much it is easy
for you to reproduce a test on it (see below for keywords to use).

Please tell at least, brand, model, model launch date (look at
Wikipedia), host, memory size, the operating system, the driver (kernel
mode and user mode), OpenGL and GLSL version, Unvanquished version you
tested, the status, the preset and the resolution you validated and
eventual notes.

If you find out the code name and related micro architecture, please
note it, same with form factor and bus.

Other data are less relevant for diagnostic and are only useful to get a
better picture of the tested hardware, don't hesitate to write down as
much info as you can.

Append the `~` character to version number if you're testing a
preversion. For example use `0.52~` to tell you tested against the
to-be-released 0.52 version.

Put a single `-` character in cell you don't have data for (do not leave
empty cells). When you describe multiple configuration for the same
piece of hardware, use the `↑` character to tell the cell uses the same
value as the previous line.

## Definitions

### Status

- **hang**: the computer becomes unresponsive, requiring a hard reset;
- **crash**: the game is terminated by the operating system on some
  unrecoverable failure;
- **missing**: the game exits by itself because of some requirement not
  being met;
- **broken**: the game loads maps but graphical bugs affecting gameplay
  are seen;
- **glitchy**: the game loads maps but graphical bugs non-affecting
  gameplay are seen;
- **slow**: the game is rendered properly but slowly with less than 30
  fps;
- **playable**: nothing wrong is noticed and frame rate is at least 30
  fps but less than 60 fps;
- **passed**: nothing wrong is noticed and frame rate is at least 60
  fps.

### Availability

- **lost**: tester has lost access to the hardware;
- **foreign**: tester has access to the hardware but does not own it;
- **unplugged**: tester owns the hardware but testing requires to plug
  the hardware in a computer;
- **unconfigured**: hardware is plugged in a computer but making use of
  it requires software changes;
- **configured**: hardware and software are ready to use for testing.

### Notes

- **extfbo**: this GPU provides instead of ;
- **fakefps**: game displays high frame rate number but the experience
  is stuttering;
- **hickups**: performance is globally correct, but sometimes the
  framerate drops a bit for a very short time;
- **lowsky**: lowering texture size using at least `r_picmip 1` is
  required to avoid skybox graphical glitches;
- **lowtex**: lowering texture size using at least `r_picmip 1` is
  required to avoid a computer hang;
- **mesamain**: running the driver from Mesa at the time of the test was
  required to get the game running or avoid major rendering bugs;
- **noaccel**: no OpenGL hardware acceleration is implemented;
- **nogather**: `GL_ARB_texture_gather` is wrongly advertised by the
  driver to be supported by this hardware, making the engine crash at
  startup (Nvidia proprietary driver bug). The engine ships some
  workaround for this driver bug, if you experience the crash on version
  0.52 and later but can properly start the game with
  `-set r_arb_texture_gather 0` engine command line option, please
  reopen issue
  [Daemon#368](https://github.com/DaemonEngine/Daemon/issues/368);
- **nohalfloatvertex**: missing `ARB_half_float_vertex` OpenGL
  extension;
- **nohyperz**: `R600_DEBUG=nohyperz` environment variable is required
  to be set to avoid graphical glitches, see issues
  [Daemon#343](https://github.com/DaemonEngine/Daemon/issues/343) and
  [Mesa#3290](https://gitlab.freedesktop.org/mesa/mesa/-/issues/3290);
- **norgtc**: `GL_ARB_texture_compression_rgtc` extension is not
  supported on this hardware, some texture may be loaded with swapped
  channels, especially normal maps. Engine implements special algorithms
  to workaround this, see issue
  [Daemon#375](https://github.com/DaemonEngine/Daemon/issues/375);
- **nvidiagarbage**: this driver is so bad you have to be very lucky to
  get at least a desktop drawn on screen before the computer hangs. With
  or without the game, after some screen freezes and display server
  crashes the kernel will complain about the card having disconnected
  itself from the PCIe bus. This issue was verified on multiple cards of
  this generations that are known to run for months without crashing
  when using free open source drivers instead;
- **slowmodel**: models with a lot of bones are known to induce severe
  frame drop on such hardware, see issue
  [Unvanquished#1207](https://github.com/Unvanquished/Unvanquished/issues/1207);
- **tinyalu**: this hardware has a very small ALU (arithmetic logic
  unit), dynamic lighting must be disabled with `r_dynamicLight 0` to
  prevent the driver to abort GLSL shader compilation that may lead to
  an engine crash, see issue
  [Daemon#344](https://github.com/DaemonEngine/Daemon/issues/344).

### Bus

- **PCI**: [Peripheral Component
  Interconnect](https://en.wikipedia.org/wiki/Peripheral_Component_Interconnect),
  slow multi-purpose bus for add-on cards, obsolete;
- **PCI-X**: [Peripheral Component Interconnect
  eXtended](https://en.wikipedia.org/wiki/PCI-X), enhanced version of
  PCI for servers and workstations, obsolete;
- **AGP**: [Accelerated Graphics
  Port](https://en.wikipedia.org/wiki/Accelerated_Graphics_Port),
  high-speed bus designed for graphic cards, obsolete;
- **FSB**: [Front-side
  bus](https://en.wikipedia.org/wiki/Front-side_bus), high-speed Intel
  system bus for CPUs, sometime used with onboard GPUs (example: GeForce
  7050 + nForce 610i/630i);
- **HT**:
  [HyperTransport](https://en.wikipedia.org/wiki/HyperTransport),
  high-speed AMD system bus for CPUs, sometime used with onboard GPUs
  (example: GeForce 6150 LE + nForce 430);
- **chip**: Internal bus of a [system on a
  chip](https://en.wikipedia.org/wiki/System_on_a_chip) (SoC), the exact
  communication bus technology is usually poorly documented;
- **PCIe**: [PCI Express](https://en.wikipedia.org/wiki/PCI_Express),
  high-speed multi-purpose bus for add-on cards and on-board devices,
  recommended;
- **CXL**: \[<https://en.wikipedia.org/wiki/Compute_Express_Link>,
  Compute Express Link\], high-speed multi-purpose bus for add-on cards;
- **TB**:
  [ThunderBolt](https://fr.wikipedia.org/wiki/Thunderbolt_(interface)),
  high speed cable combining PCI Express and DisplayPort or USB-C to
  connect external PCI Express cards like GPUs.

### Form factor

- **discrete**: full height workstation extension card, with dedicated
  graphics memory;
- **lowprofile**: low profile workstation extension card, with dedicated
  graphics memory;
- **MXM**: [Mobile PCI Express
  module](https://en.wikipedia.org/wiki/Mobile_PCI_Express_Module),
  laptop extension card, with dedicated graphics memory;
- **onboard**: dedicated GPU on motherboard, low end ones may share
  memory with the CPU;
- **integrated**: GPU integrated in CPU package or chipset, likely
  sharing memory with the CPU;
- **SoC**: System on a chip, with the GPU likely sharing memory with the
  CPU;

### Micro architecture

- **USSA**: ATi Unified Superscalar Shader Architecture;
- **GCN**: AMD Graphics Core Next;
- **RDNA**: AMD Radeon DNA;
- **GMA**: Intel Graphics Media Accelerator;
- **GT**: Intel Graphics Technology.

### Memory glossary

- **HM**: HyperMemory, ATi technology using main memory when GPU memory
  is full;
- **TC**: TurboCache, Nvidia technology using main memory when GPU
  memory is full;
- **AR**: AcceleRAM, S3 technology using main memory when GPU memory is
  full.

## Useful resources

- [Mesa Matrix](https://mesamatrix.net/)
- [Wikipedia list of AMD graphics processing
  units](https://en.wikipedia.org/wiki/List_of_AMD_graphics_processing_units)
- [Wikipedia list of AMD accelerated processing
  units](https://en.wikipedia.org/wiki/List_of_AMD_accelerated_processing_units)
- [X.Org Radeon feature matrix and decoder
  ring](https://www.x.org/wiki/RadeonFeature/)
- [Wikipedia list of Intel graphics processing
  units](https://en.wikipedia.org/wiki/List_of_Intel_graphics_processing_units)
- [Wikipedia list of Nvidia graphics processing
  units](https://en.wikipedia.org/wiki/List_of_Nvidia_graphics_processing_units)
- [Mesa Nouveau
  drivers](https://nouveau.freedesktop.org/wiki/MesaDrivers/)
- [Mesa Nouveau decoder
  ring](https://nouveau.freedesktop.org/wiki/CodeNames/)
- [User-submitted reports of OpenGL version and feature
  availability](https://opengl.gpuinfo.org/)