---
title: MinGW
permalink: /MinGW/
---

MinGW is a GCC-based compiler toolchain targeting Windows platforms. It
is used to produce the Windows releases of Unvanquished. It can be quite
complicated to use successfully, in part due to the existence of
different compiler "flavors", and confusing naming schemes. This page
serves as a guide to both MinGW in general, and specifically in
application to building Daemon and Unvanquished. Throughout this page,
"MinGW" will be used to refer to the [mingw-w64](http://mingw-w64.org/)
project, which is a fork of the (now long-moribund) "original MinGW"
project aiming to support both 32- and 64-bit builds. So beware:
something having "64" in its name does not at all imply it is for 64-bit
binaries! Same goes for "32".

## Flavors

### Bitness: 32-bit or 64-bit

Whether to compile for 32-bit ("i686" in package names) or 64-bit
("x86-64" or "x86_64") architecture. 64-bit Windows versions are capable
of running 32-bit executables in a mode called WOW (Windows-on-Windows).

### Threading flavor

You can get `win32` or `posix` thread models. Daemon must be built with
the `posix` flavor, because code that uses `std::thread` does not
compile with `win32`. In general there is no reason to use `win32`.
However, it is unfortunately the default in the APT package manager.

### Exception handling flavor

- `sjlj` (setjmp/longjmp) is available for both 32- and 64-bit builds.
  It has the drawback of significant runtime cost.
- `dwarf` is available only for 32-bit. It has good performance, but it
  is said to have a drawback that exceptions can't be propagated through
  code compiled with a different compiler (or C code?). However,
  propagating exceptions through C code shouldn't be needed for Daemon.
- `seh` (Structured Exception Handling) is available only for 64-bit. It
  has good performance and always works correctly, so it should always
  be used for 64-bit.

One way to identify which exception model code was built with is to
check the libgcc dependency. You'll find for example
`libgcc_s_seh-1.dll` for SEH, `libgcc_s_dw2-1.dll` for DWARF, or
`libgcc_s_sjlj-1.dll` for sjlj. An easy way to make a C++ test program
emit a libgcc dependency is to add a try/catch block.

### Mixing flavors

Mixing different thread or exception flavors can cause problems, such as
missing DLL dependencies, or exception handling not working.

For the `external_deps` libraries, efforts have been made to avoid
depending on any thread-flavor-specific or exception-flavor-specific
libraries, so it should be possible to use them with any flavor of
MinGW. Exception handling glitches shouldn't be an issue since the
Windows depencies are C-only.

## Distributions

### Cross-compiling from Linux

Most Linux package managers offer some form of MinGW package.
Availability of different flavor combinations varies.

#### Installation

APT (Debian Buster or older):

    # 32-bit, sjlj. win32 threads are selected by default; switch it to posix
    sudo apt install g++-mingw-w64-i686
    sudo update-alternatives --set i686-w64-mingw32-gcc /usr/bin/i686-w64-mingw32-gcc-posix
    sudo update-alternatives --set i686-w64-mingw32-g++ /usr/bin/i686-w64-mingw32-g++-posix

    # 64-bit, SEH. win32 threads are selected by default; switch it to posix
    sudo apt install g++-mingw-w64-x86-64
    sudo update-alternatives --set x86_64-w64-mingw32-gcc /usr/bin/x86_64-w64-mingw32-gcc-posix
    sudo update-alternatives --set x86_64-w64-mingw32-g++ /usr/bin/x86_64-w64-mingw32-g++-posix

APT (Debian Bullseye or newer):

- `sudo apt install gcc-mingw-w64-i686-posix` (32-bit, posix, sjlj)
- `sudo apt install gcc-mingw-w64-x86-64-posix` (64-bit, posix, SEH)

#### Usage

To build a CMake project, you need a "toolchain file". Sadly, there is
no official toolchain file from MinGW or CMake. For Daemon and
Unvanquished we use [this
(32-bit)](https://github.com/DaemonEngine/Daemon/blob/master/cmake/cross-toolchain-mingw32.cmake)
and [this
(64-bit)](https://github.com/DaemonEngine/Daemon/blob/master/cmake/cross-toolchain-mingw64.cmake).
Use it by passing `-DCMAKE_TOOLCHAIN_FILE=`<path> on the `cmake` command
line.

### MSYS2

MSYS2 runs on Windows hosts and provides up-to-date 32-bit/DWARF/posix
and 64-bit/SEH/posix toolchains. Building is done from a Bash shell in a
partial emulation of a Linux environment, similar to Cygwin.

#### Installation

Download from [1](https://www.msys2.org).

Install dependencies to build Daemon (can be done from any MSYS2 shell
flavor):

    # 32-bit
    pacman -Sy mingw-w64-i686-gcc mingw64-i686-cmake make
    # 64-bit
    pacman -Sy mingw-w64-x86_64-gcc mingw64-x86_64-cmake make

#### Usage

You must open a different MSYS2 shell flavor according to which
architecture you want to target: "MSYS2 MinGW 32-bit" or "MSYS2 MinGW
64-bit". When invoking `cmake`, you must pass the flag
`-G"MSYS Makefiles"`. When building Unvanquished, the flag
`-DDAEMON_CBSE_PYTHON_PATH=`<path> may be of interest, if you want to
use a Python other than the one shipped with MSYS2. <path> should be in
the Unix-emulation format, e.g. `/c/Python/python.exe`.

### "MinGW-W64-builds" (Standalone Windows version)

This distribution (see
[Sourceforge](https://sourceforge.net/projects/mingw-w64/)) provides a
toolchain that can be used from the Windows command prompt, without
needing a Unix emulation layer. The installer allows you to choose from
every valid combination of flavors. Caveat: the builds are currently
somewhat outdated. At the time of writing (Febrary 2021), the newest
available gcc version is 8.1.0.

#### Usage

Choose the `MinGW Makefiles` generator in CMake. The location of the
toolchain used is determined by finding the first one in your PATH
environment variable. Relative to the installation root, the PATH entry
should be at `mingw32\bin` or `mingw64\bin`.

After running CMake, compile by running `mingw32-make` in the build
directory.

#### Work around linker error with `difftime`

To build Unvanquished 0.52 or higher, a small hack is needed to avoid a
linker error, because Lua depends on an MSVCRT function which was not
added to MinGW's import lib yet as of 8.1.0. Since you are on Windows,
you can link to mscvrt.dll directly. In the CMake GUI, check "Advanced"
and find the variable `CMAKE_CXX_STANDARD_LIBRARIES`. Add
` C:/windows/system32/msvcrt.dll` at the end of the list (or
` C:/windows/syswow64/msvcrt.dll` if you are building a 32-bit binary on
a 64-bit system).

## Built-in DLL dependencies

There are a few DLLs shipped as part of MinGW that most programs will
depend on. These are also available as static libraries (a fully static
binary can be produced with the `-static` flag), but dynamic is the
default. These are:

- `libgcc`
- `libstdc++` (for C++ programs)
- `libssp` (if stack protection is enabled)
- `libwinpthread` (if threads are used)

`libstdc++` is both thread- and exception-flavor-dependent, but unlike
`libgcc`, the DLL does not have the flavor written in the filename. This
means that you can't easily tell if you have the right one (nor can the
Windows executable loader).
[Dependencies](https://github.com/lucasg/Dependencies) is a good tool to
investigate such issues.

When distributing a binary release of Daemon, you must ship these DLLs
alongside the executable, else you will run into [this
issue](https://github.com/Unvanquished/Unvanquished/issues/716). Note
that unlike Daemon's other DLL dependencies (from the `external_deps`
package), the MinGW DLLs are not automatically copied to the build
directory as part of the build process. See `extra_dll_list` and
`findDll` in the [Unvanquished release
script](https://github.com/Unvanquished/release-scripts/blob/master/build-release).

## C ABI compability with MSVC

On 32-bit x86, GCC has a different default stack alignment (16 bytes)
than MSVC (4 bytes). This can cause problems when MSVC-compiled code
calls into GCC-compiled code and the alignment is less than expected.
One solution, which we use to build MSVC-compatible `external_deps`
DLLs, is to use a GCC flag (`-mpreferred-stack-boundary=`) to change the
presumed stack alignment. Another, which we use to handle jumps from
3rd-party binaries to our (MinGW-built) code, is to put the annotation
`__attribute__((force_align_arg_pointer))` on the functions which may be
called with less alignment than expected, instructing the compiler to
perform alignment when the function is called.

`-mms-bitfields` should be enabled to ensure that the layout of structs
containing bitfields matches. This is on by default.