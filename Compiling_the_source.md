---
title: Compiling the source
permalink: /Compiling_the_source/
---

## Dependencies

The game requires some dependencies to be built, which are the same on
all systems:

- cmake
- python3-yaml
- python3-jinja2
- A C++11 able compiler (those are known to work: clang (\>= 3.5), gcc
  (\>= 4.8), visual studio (\>= 2019))
- zlib1g
- libgmp
- nettle
- libcurl4-gnutls
- libsdl2
- libglew
- libpng
- libjpeg-turbo8
- libwebp
- libfreetype6
- liblua5.3
- libopenal
- libogg
- libvorbis
- libopusfile

Those are optional:

- libncursesw5

## macOS

First, you need to [acquire the source
code](Getting_the_source "wikilink").

Regardless of what interface you may use to compile the source, you will
need [CMake](http://www.cmake.org/cmake/resources/software.html) to
generate makefiles. You will also need to install
[Xcode](https://developer.apple.com/xcode/). At a minimum, you must
install the "Xcode command-line tools" in order to compile anything. You
may also install Xcode proper, if you wish to use that IDE.

Once you have the source code and the tools installed, you may actually
proceed to compile the source. You have several options:

- **Compile the source at the command line**. This is the easiest if you
  would just like to compile the game to use yourself and you do not
  intend to work on the code.
- **Compile the source using an IDE**. This is preferred if you intend
  on developing the source.
  - Xcode is Apple's flagship IDE.
  - [QtCreator](http://qt-project.org/downloads) is cross-platform and
    provides real-time feedback of syntax errors, a Vim mode, as well as
    other features.
  - [Code::Blocks](http://www.codeblocks.org/) is also cross-platform
    but lacks some of the features of Xcode and QtCreator.

### Dependencies

Precompiled static libs are provided for all dependencies. CMake
downloads them at configure time and extracts to
`daemon/external_deps/macos-amd64-default_`<i><version></i>`/`. These
were produced by the `external_deps/build.sh` script, which you could
also use to build them yourself if you want to for some reason.

### Configuring with CMake

1.  Run CMake.
2.  Enter the location of the source code.
3.  Enter the location in which you would like to build the source code.
    This should be a different directory.
4.  Click "Configure". You will be prompted as to which generator you
    would like to use. If you have Xcode installed, choose that. Wait
    while the configuration process runs. You may have to set the
    following:
    1.  If you have selected to generate Xcode project files, make the
        `SDLMAIN_LIBRARY` field blank. This option is not available if
        you have the generator set to Unix makefiles.
5.  Click "Generate".
6.  You may now close CMake.

### Compiling

#### With Xcode

1.  Either start Xcode and open the project file (in the build directory
    you specified) or double-click the project file in Finder.
2.  Open the project file created by CMake, which should be in the build
    directory you specified.
3.  Change the active target to "ALL_BUILD" and click Product→Build.

#### With Unix Makefiles

- Start Terminal (Applications → Utilities → Terminal).
- Type the following commands:
      $ cd /path/to/Unvanquished-build
      $ make

  If you are on a multi-core or multi-processor machine, you may speed
  up the process by passing the `-j` argument followed by the number of
  available cores to `make`; e.g., `make -j4`. Note that doing so makes
  reading error messages more difficult, as multiple instances of the
  compiler will print to the screen at once, causing information to
  appear out of order.

### Testing the build

#### With Xcode 4

To test the game, select the "client" scheme from the combo box on the
toolbar, and click the run button or press .

### Bundling the Application

#### With CPack

CPack is able to create standalone bundles (as well as many other types
of installers). However you must generate the files using Unix Makefiles
instead of Xcode.

`$ cd /path/to/Unvanquished-build`
`$ cpack -G Bundle`

Some warnings will be printed however these can be safely ignored. There
should be a file called Unvanquished.dmg in the Unvanquished-build
folder.

#### Manually

You'll find the Mac [dynamic library
bundler](http://macdylibbundler.sourceforge.net/) to be quite useful
(you must generate the files using Unix Makefiles instead of Xcode):

`$ curl -L `[`http://sourceforge.net/projects/macdylibbundler/files/macdylibbundler/0.4.1/dylibbundler0.4.1.zip/download`](http://sourceforge.net/projects/macdylibbundler/files/macdylibbundler/0.4.1/dylibbundler0.4.1.zip/download)` > \`
`   dylibbundler0.4.1.zip`
`$ unzip dylibbundler0.4.1.zip`
`$ cd dylibbundler`
`$ make`
`$ sudo make install`

Once you've done that, you can proceed to create the application bundle.
Note that these steps assume that you have downloaded the data files to
`main/` as shown above:

    $ git=/path/to/Unvanquished-git-repo
    $ build=/path/to/Unvanquished-build-dir
    $ mkdir -pv Unvanquished.app/Contents/{libs,MacOS,Resources,Frameworks}
    $ cp -r $build/main Unvanquished.app/Contents/MacOS
    $ sips -s format tiff $git/debian/unvanquished.png --out temp.tiff
    $ tiff2icns temp.tiff Unvanquished.app/Contents/Resources/Unvanquished.icns
    $ rm temp.tiff
    $ cp $build/daemon{,ded}.i386 $build/*.dylib Unvanquished.app/Contents/MacOS
    $ cp -r /Library/Frameworks/SDL.framework Unvanquished.app/Contents/Frameworks
    $ install_name_tool -id \
        @executable_path/../Frameworks/SDL.framework/Versions/A/SDL \
        Unvanquished.app/Contents/Frameworks/SDL.framework/Versions/A/SDL
    $ install_name_tool -change @rpath/SDL.framework/Versions/A/SDL \
        @executable_path/../Frameworks/SDL.framework/Versions/A/SDL \
        Unvanquished.app/Contents/MacOS/daemon.i386
    $ install_name_tool -change @rpath/SDL.framework/Versions/A/SDL \
        @executable_path/../Frameworks/SDL.framework/Versions/A/SDL \
        Unvanquished.app/Contents/MacOS/librendererGLi386.dylib
    $ install_name_tool -change @rpath/SDL.framework/Versions/A/SDL \
        @executable_path/../Frameworks/SDL.framework/Versions/A/SDL \
        Unvanquished.app/Contents/MacOS/librendererGL3i386.dylib
    $ for binary in Unvanquished.app/Contents/MacOS/*.{i386,dylib}; do
        dylibbundler -b -x $binary -d $dest/Unvanquished.app/Contents/libs/; done
    $ cp /usr/lib/libGLEW.1.7.0.dylib ./Unvanquished.app/Contents/libs/libGLEW.1.7.0.dylib
    $ chmod +w ./Unvanquished.app/Contents/libs/libGLEW.1.7.0.dylib
    $ install_name_tool -id @executable_path/../libs/libGLEW.1.7.0.dylib \
        ./Unvanquished.app/Contents/libs/libGLEW.1.7.0.dylib
    $ install_name_tool -change /usr/lib/libGLEW.1.7.0.dylib \
        @executable_path/../libs/libGLEW.1.7.0.dylib \
        ./Unvanquished.app/Contents/MacOS/daemon.i386
    $ cat > Unvanquished.app/Contents/Info.plist <<\EOF
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
              "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
    <plist version="1.0">
    <dict>
        <key>CFBundleName</key>
        <string>Unvanquished</string>
        <key>CFBundleDisplayName</key>
        <string>Unvanquished</string>
        <key>CFBundleExecutable</key>
        <string>daemon.i386</string>
        <key>CFBundleIconFile</key>
        <string>Unvanquished.icns</string>
        <key>CFBundleIdentifier</key>
        <string>net.Unvanquished</string>
        <key>CFBundleInfoDictionaryVersion</key>
        <string>6.0</string>
        <key>CFBundlePackageType</key>
        <string>APPL</string>
        <key>CFBundleShortVersionString</key>
        <string>0.4.0</string>
        <key>CFBundleVersion</key>
        <string>0.4.0</string>
    </dict>
    </plist>
    EOF

The contents of the completed application bundle should look like this:

<figure>
<img src="Bundle_dir_Mac_OS_X.png"
title="File:Bundle_dir_Mac_OS_X.png" />
<figcaption><a
href="File:Bundle_dir_Mac_OS_X.png">File:Bundle_dir_Mac_OS_X.png</a></figcaption>
</figure>

**Note**: If you compiled SDL from source, you will not see a directory
titled `SDL.framework`.

## Windows

### Visual Studio

CMake can generate Visual Studio projects for Unvanquished.

1.  Add _NO_DEBUG_HEAP=1 to your environment variables otherwise
    performance under the debugger [will be
    terrible](http://www.massimpressionsprojects.com/dev/altdevblog/2011/07/27/the-unexpected-performance-of-debug-builds/)
2.  Run CMake with the source directory as the base directory of your
    source code (which should contain the directory `src`), and the
    build directory as a subdirectory of the source directory named
    `build`.
3.  Click the <b>Open Project</b> button. Or if you used CMake from the
    command line, open `build/Unvanquished.sln` in Visual Studio.
4.  In Visual Studio, choose your desired build type (default:
    <b>Debug</b>) from the drop-down menu in the top bar. <b>Debug</b>
    runs assertions and has complete debug information, but is slower.
    <b>RelWithDebInfo</b> is fast and still fairly usable with the
    debugger, but assertions don't run and sometimes you can't see the
    value of a local variable.
5.  Use Build → Build Solution to compile the code. Or just press to
    build and run, but beware: this will not automatically build cgame
    or sgame! Only engine changes are automatically rebuilt when you run
    something from Visual Studio.

#### Important Notes

- Due to limitations with CMake, the startup project cannot be
  specified. This must be set manually to debug the client with Visual
  Studio:
  - Right click on client and select "Set as Startup project".

### MinGW

It is possible to produce a Windows build of Unvanquished with
[MinGW](MinGW "wikilink"), as either a Windows or a Linux user. See
[MinGW#Distributions](MinGW#Distributions "wikilink") for detailed
information about the toolchains available for installation.

#### Instructions for native Windows build with MSYS2

1.  Install MSYS2.
2.  Open the *MSYS2 MinGW 32-bit* or *MSYS2 MinGW 64-bit* terminal,
    depending on which bitness you want to build.

</li>

Install toolchain:

    # For 32-bit replace x86_64 with i686
    pacman -Sy && pacman -S mingw-w64-x86_64-gcc mingw-w64-x86_64-cmake make

</li>
<li>

Run CMake. If you're building Unvanquished, you may want to use the
`-DDAEMON_CBSE_PYTHON_PATH=`<path> option in case you want to use a
different Python rather than the one in MSYS2.

    mkdir mybuild && cd mybuild
    cmake -G "MSYS Makefiles" somepath/Unvanquished

</li>
<li>

Build:

     make -j4

If you would like verbose output (useful to see compiler flags), set the
`VERBOSE` environment variable before running Make.

    export VERBOSE=1

</li>
</ol>

You may find that the game (or some part of the MSYS2 toolchain!) fails
to start due to missing DLL dependencies. Two helpful tools are:

- The strace command in MSYS2, e.g. `strace ./daemon`
- [Dependencies](https://github.com/lucasg/Dependencies) (a Windows GUI
  program)

When distributing MinGW binaries, you need to distribute some additional
DLLs besides the ones in the build folder. See
[MinGW#Built-in_DLL_dependencies](MinGW#Built-in_DLL_dependencies "wikilink").

#### MSYS2 Clang

In MSYS2, it is possible to build with Clang, rather than GCC as shown
as in the above instructions. However, some of our pre-built libraries
are incompatible. You need to use the ones from pacman instead.

1.  Create a deps folder with incompatible packages removed. This
    assumes that the latest version of the prebuilt deps for the mingw
    package of the appropriate bitness has already been extracted to the
    `windows-${ARCH}-mingw_${VERSION}` directory. In this example, we
    use `windows-amd64-mingw_8`.
        cd somepath/daemon/external_deps
        mkdir msysclang
        cp windows-amd64-mingw_8 -R msysclang
        find msysclang -depth -name '*freetype*' -o -name '*png*' -o name '*curl*' -o -name '*lua*' | grep -v pnacl | xargs rm -r
2.  Install those deps from Pacman:
        # For Daemon
        pacman -Sy && pacman -S mingw-w64-clang-x86_64-freetype mingw-w64-clang-x86_64-curl mingw-w64-clang-x86_64-libpng
        # For Unvanquished
        pacman -Sy && pacman -S mingw-w64-clang-x86_64-freetype mingw-w64-clang-x86_64-lua
3.  Use the deps folder you made when configuring the build:
        CC=clang CXX=clang++ cmake -G "MSYS Makefiles" -DEXTERNAL_DEPS_DIR=somepath/daemon/external_deps/msysclang /c/path/to/source

    If you see a download progress bar upon invoking CMake, you did the
    deps stuff wrong.

### QtCreator

1.  Install MinGW and follow the above instructions, except select
    Code::Blocks as the generator.
2.  Start QtCreator, and select "Open File or Project…" from the File
    menu.
3.  Navigate to your source directory and open CMakeLists.txt.
4.  At the CMake Wizard, select the same build directory you already
    configured using CMake. (If you did not chose Code::Blocks as the
    generator, you will have to start over again, as QtCreator requires
    a Code::Blocks project file in order to compile the source.)
5.  Ensure that a generator is selected in the combo box, and click "Run
    CMake". If there is no generator listed, see the
    [troubleshooting](#Troubleshooting "wikilink") section below.
6.  Click "Finish" to close the wizard.

You should now be able to compile, run, and debug the code using
QtCreator.

#### Troubleshooting

If at the "Run CMake" prompt of the the CMake Wizard, select "Run CMake"
and are warned that no generator was selected, and notice that there are
no generators in the combo box, you will likely have to [manually
configure your
toolchain](http://doc.qt.digia.com/qtcreator-2.4/creator-tool-chains.html).
Select "Options…" from the "Tools" menu, then navigate to "Build & Run".

At the options window,

- Go to the "Kits" tab, and mouse over the "Desktop (default)" kit under
  "Manual". If there were any errors in configuring this kit, they will
  be displayed in the tool tip. If there are problems, select the kit.
  You may need to manually specify the location of the MinGW debugger,
  for example, which is typically `C:\MinGW\bin\gdb.exe`.
- Go to the "Compilers" tab, and ensure that MinGW is present. If not,
  you will need to add it manually.

## Linux

### Dependencies

#### Debian/Ubuntu

`sudo apt-get install build-essential cmake libcurl4-gnutls-dev \`
` libglew-dev libgmp-dev nettle-dev zlib1g-dev libncursesw5-dev \`
` libsdl2-dev libopenal-dev libjpeg-dev libpng-dev libwebp-dev \`
` libogg-dev libvorbis-dev libopusfile-dev \`
` libfreetype6-dev \`
` liblua5.3-dev \`
` python3-yaml python3-jinja2`

If the version of WebP supplied by your version of Debian or Ubuntu is
older than v0.2.0, you will need to
[download](https://code.google.com/p/webp/downloads/detail?name=libwebp-0.2.0.tar.gz)
and [compile it from
source](https://developers.google.com/speed/webp/docs/compiling#unix).
After compiling and installing with `sudo make install`, in CMake,
you'll need to set `WEBP_INCLUDE_DIR` to `/usr/local/include/webp` and
`WEBP_LIBRARY` to `/usr/local/lib/libwebp.so`.

Developpment package name may differs, for example `libgmp-dev` may be
named `libgmp3-dev` and `libglew-dev` may be named `libglew1.7-dev`.

We have a `debian` directory in the source tree, you can check what's
missing this way.

`cd `<var>`path/to/unvanquished`</var>
`dpkg-checkbuilddeps`

Then install the listed packages this way:

`sudo apt-get install `<var>`package list`</var>

The `dpkg-checkbuilddeps` command produces no output if you already have
the required dependencies.

Note that you only need `debhelper` to build `.deb` files.

#### Fedora

(This was tested to work on fedora 22 workstation)

`$ sudo dnf install \`
`  cmake gcc gcc-c++ \`
`  {glew,gmp,lua,mesa-libGL,ncurses,nettle,openal-soft,opus,opusfile,SDL2,speex}-devel \`
`  lib{curl,jpeg-turbo,png12,vorbis,webp}-devel`

#### Gentoo

`$ emerge curl freetype glew gmp jpeg ncurses libogg openal libpng libsdl libvorbis zlib`

#### openSUSE

`$ sudo install zypper gcc gcc-c++ Mesa-libGL-devel SDL-devel libjpeg8-devel \`
`  libpng12-devel glew-devel webp-devel ncurses-devel gmp-devel libcurl-devel \`
`  libnettle-devel openal-soft-devel speex-devel libvorbis-devel`

The latest version of WebP must be installed manually (FIXME: why, if
there is webp-devel in the zypper package list?):

`$ cd Unvanquished/daemon/external_deps`
`$ ./build.sh linux-amd64-default webp naclsdk naclports`
`$ ./build.sh linux-amd64-default install`

You must disable curses (set `USE_CURSES` appropriately in CMake) as
failing to do so will cause Unvanquished to crash on startup.

### Configuring the code with CMake

After you have [acquired the source
code](Getting_the_source "wikilink"), you can proceed to compile.
Unvanquished uses CMake, so you must have that installed.

#### Using ccmake (curses-based front-end)

On Debian or Ubuntu:

`$ sudo apt-get install cmake-curses-gui`

On Gentoo you should set the **ncurses** USE flag either globally or
individually, just for cmake. To add the USE flag globally, edit the USE
array in /etc/make.conf for it to include **ncurses**. To only install
cmake with ncurses functionality, you could do the following:

`$ echo 'dev-util/cmake ncurses' >> /etc/portage/package.use && emerge cmake`

Note that in Ubuntu, `cmake-curses-gui` is in Universe, which you may
have to enable with `software-properties-gtk`. Make sure to reload the
software sources with `sudo apt-get update` afterwards.

Optionally: to use clang (rather than the default gcc and g++ compilers)
export the CC and CXX variables before running cmake:

`$ export CC="clang"`
`$ export CXX="clang++ -stdlib=libc++ -lc++abi"`

Next, configure the codebase.

`$ cd `<var>`/path/to/unvanquished`</var>
`$ mkdir build`
`$ cd build`
`$ ccmake ..`

In Debian or Ubuntu you can build a package this way (you need
`devscripts` and `fakeroot` packages):

`$ cd `<var>`/path/to/unvanquished`</var>
`$ fakeroot dpkg-buildpackage -b -uc`
`$ sudo dpkg -i `<var>`../unvanquished_*.deb`</var>

Once in `ccmake`, use the following keys:

- Press to configure. If an error occurs during this phase, make note of
  it and press to dismiss it.
- Use the up and down arrow keys to navigate the compilation options.
- Press to enable or disable boolean options (i.e., on/off) or to edit
  textual options.
  - Press when editing a textual option to cancel the change.

Once you have finished the configuration process, press again, then to
generate the makefile.

#### Using cmake-qt-gui (graphical front-end)

This graphical front end for cmake has its own package you must install:

##### Debian/Ubuntu

`$ sudo apt-get install cmake-qt-gui`

##### Gentoo

With the **qt4** USE flag enabled:

`$ emerge cmake`

Once installed, run with `cmake-gui`.

<figure>
<img src="Cmake-qt-gui.png" title="Cmake-qt-gui.png" />
<figcaption>Cmake-qt-gui.png</figcaption>
</figure>

1.  Set the path where you have the source code downloaded.
2.  Set the path where you would like to build the engine. This may be
    the same directory if you wish.
3.  Click 'Configure'.
4.  Click 'Generate'.

#### Unnecessary libraries

Regardless of which front-end to cmake you use, you may want to disable
some libraries that are not strictly necessary:

- `USE_BREAKPAD` — Disabling this will cause the game to not produce
  crashdumps on failure.
- `USE_CURSES` — Disabling this will cause the external (not in-game)
  console to not use curses; it will not be scrollable and will be
  similar to the console in the original Tremulous. This does in no way
  affect gameplay.

### Compiling

`$ cd `<var>`path/to/unvanquished/build`</var>
`$ make -j4`

The `-j` switch to make allows you to speed up the compilation process
by running it in multiple threads; set the number following this to the
number of cores your processor(s) have.

## Acquiring the Game Files

### Acquiring mandatory game files

The game files are not in the Git repository, and must be downloaded
separately. They must be saved to the [data
location](Game_locations "wikilink") for your system.

Linux users may use the `download-paks` script that is distributed with
the source code, which requires one of curl, wget or aria2 to be
installed:

`$ cd `<var>`path/to/unvanquished/build`</var>
`$ ../download-paks pkg`

Otherwise, the set of necessary packages can be extracted from the
[latest release](https://github.com/Unvanquished/Unvanquished/releases),
or downloaded a la carte from the [package
index](http://dl.unvanquished.net/pkg/).