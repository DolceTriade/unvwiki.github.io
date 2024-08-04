---
title: Technical Documentation
permalink: /Technical_Documentation/
---

This Wiki page is incomplete and a work-in-progress, nonetheless there
is still helpful information on this web page.

If you have a question that is not answered here, you can always hop on
[IRC](IRC "wikilink").

## Basic architecture

The is very minimal and is basically a game loader. It has access to the
file system, network, graphics card, sound, and runs the virtual machine
hosting the game code. Many things are living in the game code itself:
Artificial Intelligence (AI), User Interface (UI), particles, trails…

While the end user is only starting the engine to run the game, under
the hood the engine and the game are two executables running in parallel
and talking to each others using an IPC. The game itself runs isolated
in a virtual machine, giving data to the engine to process or giving
orders to the engine to do this or that. This makes possible for game
servers to provide custom game codes (mods) to users without the ability
for the said mod to access things from outside of the game.

<table>
<thead>
<tr class="header">
<th><p>Daemon (engine <ins>code</ins>)</p></th>
<th><p>Unvanquished (game <ins>code</ins>)</p></th>
<th><p>UnvanquishedAssets (game <ins>data</ins>)</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>Virtual machine (NativeClient)</li>
<li>File system (System, )</li>
<li>Networking</li>
<li>OpenAL, Sound effects</li>
<li>OpenGL, shaders</li>
<li><p>map format</p></li>
<li><p>formats</p></li>
<li><p>formats</p></li>
<li><p>formats and animations</p></li>
<li><p>format</p></li>
</ul></td>
<td><ul>
<li>UI (RmlUi)</li>
<li><p>format</p></li>
<li><p>format</p></li>
<li>Model skinning</li>
<li>Minimap display</li>
<li>AI: , , </li>
<li><a href="Server_Map_layout" title="wikilink">Map layout</a>, <a
href="Server_Map_rotation" title="wikilink">Map rotation</a></li>
<li>Player moves</li>
<li>Weapon mechanisms</li>
<li>Buildable mechanisms</li>
<li>Game logic</li>
</ul></td>
<td><ul>
<li>UI files (RML, RCSS…)</li>
<li>Common materials:<br />
ladder, noclip, nobuild…</li>
<li>Maps (game levels)</li>
<li>Texture sets: Image, Material files,<br />
Skyboxes</li>
<li>Sound sets: Music, Sound files</li>
<li>Resource sets: Models, Skin,<br />
Images, Materials files,<br />
Trail, Particle files,<br />
Sound files</li>
</ul></td>
</tr>
</tbody>
</table>

When making a game based on the Dæmon engine, you may want to also use
the *Unvanquished* repository as an upstream to benefit from all the
generic features like particles, trails, navmesh, and things like that.
Rebasing or merging updates from upstream will keep your game updated
with latest features and fixes for common parts.

See also: [Formats](Formats "wikilink").

## Getting Started

If you have not already, go [get the
code](Getting_the_source "wikilink"), read up on your options for
[development environments](development_environments "wikilink"), and
[compile it](Compiling_the_source "wikilink"). Instructions are
available for a variety of platforms. If your platform of choice is not
listed, you are welcome to add instructions for it.

From there, play the game! The [Running the
game](Running_the_game "wikilink") page contains documentation on all
the most commonly used and user-accessible commands and console
variables. If you have trouble, see the
[troubleshooting](troubleshooting "wikilink") page for possible
solutions.

There are also very detailed instructions on [testing the
game](Testing "wikilink"), which includes information on using
sophisticated profiling tools such as apitrace, GPUPerfStudio,
gDEBugger, valgrind, and clang-analyzer.

### Need something to work on?

There are all sorts of existing tasks listed on our [issues reported on
the bug tracker](https://github.com/Unvanquished/Unvanquished/issues)
you are free to fix. Please drop in on [IRC](IRC "wikilink") and tell us
what you're up to.

### Giving Back

You are welcome to contribute in any way possible! We have [guidelines
for contributing code](Contributing_Code "wikilink") as well as
documentation on [coding conventions](Coding_convention "wikilink").

### Notes

If you are attempting to generate the Microsoft Visual Studio solution
file for the Unvanquished game system make sure you have installed all
Python related dependencies for cmake to generate the solution file. If
cmake fails to generate the solution file because of alleged missing
Python dependencies but you know you have them for a fact then check the
cmake variable `_Python_EXECUTABLE_` that its value is set to the
location of the Python executable of the Python installation having the
dependencies, for example "C:\Program Files\Python39\python.exe" and not
the Python executable obtained from the Windows App Store "C:\Program
Files\WindowsApps\\..". Pip would install Python dependencies for the
non-Windows App Store executable.

## Language Oddities

- You should cast integers that are being used as enum values to an enum
  type. For example:
      BG_Class( static_cast<class_t>( self->client->ps.stats[STAT_CLASS] )

## Modder Documentation

### classes_.attr

<https://wiki.unvanquished.net/wiki/Modder_Documentation:_classes_.attr.cfg>

## Source Code Tree and File Descriptions

- `pkg/` - game assets
  - `unvanquished_src.dpkdir`
    - `fonts/`
    - `gfx/`
    - `lights/`
    - `models/`
    - `scripts/`
    - `sound/`
    - `translation/`
    - `ui/`
- `daemon/` - engine submodule
  - `src/` - engine source code
    - `shared/`
    - `server/`
      - `sg_api` - contains definitions for the VM to engine
        function-procedures
      - `CommonProxies` - proxy interface to the VM, has trap calls for
        sending messages to the VM
    - `common/`
      - `Cvar` - the proxy interface for console variables
      - `Debugger` - contains a routine to detect if a debugger is
        attached to the process
      - `FileSystem` - interface to use the host filesystem through the
        VM
      - `KeyIdentification` - contains an association table (unordered
        map) that links a keyboard key value with a string descriptor
      - `LineEditData` - ?
      - `Log` - filesystem logging
      - `IPC/`
        - `Common` - common definitions for all IPC methods
        - `Command` - the inter-process communication command buffer
        - `Channel` - contains the inter-process communication namespace
          and engine-VM messaging functions
        - `Primitives` - routines for the IPC VM-engine socket
      - `CM/` - related to game collisions and map loading
        - `cm_local`
        - `cm_patch`
        - `cm_polylib`
        - `cm_public`
      - `Color` - related to colors
    - `engine/`
      - `audio/`
      - `botlib/`
      - `client/`
      - `crash_server/`
      - `framework/`
      - `null/`
      - `qcommon/` - common code: utility functions, typedefs, macros,
        and the like
        - `q_shared.h` - included first by ALL program modules. A user
          mod should never modify this file.
        - `q_shared.cpp` - stateless support routines that are included
          in each code module
        - `q_math` - stateless support routines that are included in
          each code module, related to math operations
        - `q_Unicode` - Unicode & UTF-8 handling
      - `renderer/` - renderer
        - `glsl_source/` - OpenGL shader code
      - `server/`
        - `sv_sgame` - interface to the game module
      - `sys/`
    - `shared/`
      - `client/`
      - `server/`
  - `src/` - the sources for the game-logic modules, both Client and
    Server
    - `cgame/` - client-local game-logic code
    - `sgame/` - server-local game-logic code
      - `botlib/` - directory containing sources for bot AI
        - `bot_api` - forward function declarations related to the bot
          artificial intelligence code
        - `bot_convert` - procedures for the conversation
        - `bot_local` - server-local variable definitions, struct
          definitions, and forward declarations for the bot AI
        - `bot_navdraw` - code for drawing bot AI navmesh for debug
          purposes
        - `bot_types` - code that defines data types for bot AI code
      - `Components/` - directory containing the sources for the CBSE
        entity components
        - `AcidTubeComponent` - code for Acid Tube entity component
        - `AlienBuildableComponent` - code for alien buildable entity
          component
        - `AlienClassComponent` - code for alien class entity component
        - `ArmourComponent` - the armour entity component class
        - `ArmouryComponent` - the armory entity component class
        - `BarricadeComponent` - the code for the barricade entity
          component
        - `BoosterComponent` - the booster component entity component
          class
        - `BuildableComponent` - code for the buildable entity component
          class
        - `DeferredFreeingComponent` - code for the deferred freeing
          component
        - `DrillComponent` - code for the drill entity component
        - `EggComponent` - code for the egg entity component
        - `HealthComponent` - the health component for a CBSE entity
        - `HiveComponent` - the hive component for a CBSE entity
        - `HumanBuildableComponent` - the human buildable component for
          a CBSE entity
        - `HumanClassComponent` - the human class component for a CBSE
          entity
        - `IgnitableComponent` - the ignitable component for a CBSE
          entity
        - `KnockbackComponent` - the knockback component for a CBSE
          entity
        - `LeechComponent` - the leech component for a CBSE entity
        - `MainBuildableComponent` - the main buildable component for a
          CBSE entity
        - `MedipadComponent` - the medi pad component for a CBSE entity
        - `MGTurretComponent` - the MG turret component for a CBSE
          entity
        - `MiningComponent` - the mining component for a CBSE entity
        - `OvermindComponent` - the overmind component for a CBSE entity
        - `ReactorComponent` - the reactor component for a CBSE entity
        - `RocketpodComponent` - the rocket pod component for a CBSE
          entity
      - `CBSE` - the files containing the core entity declarations and
        definitions
        - `CBSE.h` - connects a source files to the CBSE backend and
          provides all needed types to CBSE
        - `CBSEBackend` - has the declaration of the base entity,
          implementation of the base components, and helper routines to
          access entities and components
        - `CBSEComponents.h` - files with all game entity component
          headers
        - `CBSEEntities.h` - specific entity declarations
      - `Assert` - daemon engine specific assert code
      - `Clustering` - has code related to the (literal) clustering of
        base buildables
      - `sg_active` - process server-local game events and server-local
        client effects
      - `sg_client` - server-local functions for a client
      - `sg_entities` - server functions for server-local game entities
      - `sg_main` - core server game functions
      - `sg_utils` - misc utility functions for game module
      - `sg_team` - function-procedures related to game teams
      - `sg_local` - header file with more header inclusions
      - `sg_svcmds` - this file holds commands that can be executed by
        the server console, but not remote clients
      - `sg_spawn` - contains the declarations of the spawn functions
        for various game map entities
      - `sg_session` - code for client session data
      - `sg_physics` - game physics code
      - `sg_admin` - server admin management code
      - `sg_namelog` - record client names that connect to the server
      - `sg_api` - contains the interface for the server game-logic
        module to handle messages received from the VM
      - `Entities` - contains helper routines for CBSE entity components
    - `shared/`
      - `bg_public` - definitions shared by both the server game and
        client game modules
      - `bg_local` - local definitions for the bg (both games) files
      - `bg_gameplay` - gameplay related macro constants and external
        variable linkage
      - `parse` - parsing game script files
    - `utils/`

## System Architecture

**General:** The architecture of the Daemon game engine is fundamentally
the Client and Server architecture. In essence the Client uses a service
provided by the Server. In the case of Daemon and Unvanquished, the
service is the game Unvanquished and the Client receives this game when
the Client connects to the game Server. The Client and Server are two
different programs executed on the computer, the Client is "daemon.exe"
and the Server is "daemonded.exe". This separation into two different
programs makes it possible for the Server program to be executed on a
machine as part of another computer network connected to the Internet so
the Server and Client does not necessarily execute on the same computer
machine but the same machine can execute both Client and Server (hence
'local' game, the Client connects to the server running on the host
machine "127.0.0.1").

The Client and Server do different things. The Client has the task of
receiving input by the user then updates its game-state per this input
(for example, the player using their keyboard to move the character
forward some distance) then transmit these input events to the Server,
and to actually draw the computer graphics, etc. The Server has the task
of simulating the game itself but does not render any graphics for a
user, for example game objects would exist on the Server, and the Server
would tell the Client that game object exists and it should be drawn on
the screen. These examples are not all functionalities the Client or
Server performs. Each entity in this relationship keeps separate game
states and these game states must be synchronized, whatever happens on
the side of the Server game is transmitted to the Client as game updates
and anything the Client needs to happen must be transmitted to the
Server as client commands, for example the user moving their controlled
character somewhere else in the level, these movements would be
transmitted as commands to the Server to update its game state with the
new player location. Quake III (and so Daemon) does this synchronization
efficiently, the client receives a snapshot (a program object that
contains data about the server's game state since the time the snapshot
was sent to the client) and the client updates this snapshot with
'deltas' it receives from the server, these deltas are updates or
changes to the server game state and only these changes are transmitted.

**The Virtual Machines:** The Daemon and Unvanquished systems are
ultimately descendants of the original Quake III Arena game engine known
as Id Tech 3. The Id Tech 3 game engine has a virtual machine
incorporated into the executable program and functions as an
intermediary between the actual game logic code and the engine. The game
logic system interfaces with the virtual machine to invoke engine
functionalities, the game code does not invoke engine functions itself,
the virtual machine does that action. Communication between the game
code and the engine happens via Inter-Process Communication (IPC)
through special pipe files, the engine sends messages to a virtual
machine and the virtual machine invokes game code functions according to
the type of message it receives from the engine. The game logic sends
messages to the virtual machine to invoke engine functions. The client
subsystem of Daemon has its own virtual machine and the server subsystem
of Daemon has its own virtual machine.

**Code Categorization:** The code of Daemon and Unvanquished are 2
categories: the engine system code the game Unvanquished is based on and
the actual game-logic code that defines playable game objects and
gameplay. The Daemon engine and the virtual machines are in the system
code category while the Unvanquished game code is in the game-logic code
category.

## Client

The function of the Client is to receive input events generated by the
human user and transmit these events to the Server, and to draw computer
generated graphics to the user's screen.

Input is received through SDL input capture, see the function
`void IN_Frame()` of *daemon/src/engine/sys/SDL_Input.cpp*.

## Program Ignition and Initialization

The engine system is compiled into a static library (.lib file) and
linked into (incorporated) the client executable ("daemon.exe") (and the
server executable "daemonded.exe"), this means that when the program
(application) is started by double-clicking the file in the WindowsOS
GUI the engine is loaded into memory.

The entry point into the game system is the function
`ALIGN_STACK_FOR_MINGW int main(int `*`argc`*`, char** `*`argv`*`)` in
the file System.cpp at line 666 (as of the latest Github commit for 28
June 2021
[1](https://github.com/DaemonEngine/Daemon/blob/b5e4eedca774adddb8f786851966def7e29680c7/src/engine/framework/System.cpp#L666)).
This function is called by SDL and is macro defined as SDL_main (see
SDL_main.h, lines 120-121).

Main (SDL_main) calls
`static void Init(int `*`argc`*`, char** `*`argv`*`)` in the file
System.cpp at line 525 (as of the latest Github commit for 28 June 2021
[2](https://github.com/DaemonEngine/Daemon/blob/b5e4eedca774adddb8f786851966def7e29680c7/src/engine/framework/System.cpp#L525)),
this function initializes the engine and any error that happens here is
fatal. As part of the initialization procedure, a special pipe file is
created within the base game directory file tree structure, the game
communicates with the engine through this pipe file, both the engine
system and game system shares this pipe file to communicate data to each
other.

**Initialization for Virtual Machines:** There are two virtual machines
as parts of the Daemon and Unvanquished game systems: **CGameVM** and
**GameVM**. **CGameVM** is the virtual machine for the client and
**GameVM** is the virtual machine for the server. See
daemon/src/engine/client/client.h for the class declaration of the
client VM and daemon/src/engine/server/server.h for the class
declaration of the server VM.

The client VM is created with a call to `CGameVM::Start()` and this is
called from `void CL_StartHunkUsers()` or
`void CL_Disconnect( bool `*`showMainMenu`*` )`. See
daemon/src/engine/client/cl_cgame.cpp.

The server VM is created with a call to `void GameVM::Start()` and this
is called from `void SV_InitGameProgs()` and this is called from
`void SV_SpawnServer(std::string `*`pakname`*`, std::string `*`mapname`*`)`.
The server VM is created when the server game starts running. See
daemon/src/engine/server/sv_init.cpp.

**Initialization for Game-Logic Modules:** The game-logic modules are
themselves programs and have a main entrance function of
`int main(int `*`argc`*`, char** `*`argv`*`)` of VMMain.cpp at line 120,
this is true only if the client and server are built as executables,
this code is not compiled if the client and server are compiled into
dynamic link libraries (dlls). All game-logic modules must have a main
function. This main function is the first function called in the program
and begins the initialization process. The virtual machine starts
game-logic module execution by creating a sub-process via the operating
system with a call to the function *CreateProcessW()* (see
daemon/src/engine/framework/VirtualMachine.cpp at line 152 inside the
function *InternalLoadModule*).

The server game is not started until a map is loaded.

This entry point is called by the virtual machine for the game-logic
module (for example: the client virtual machine invokes **Main** of
VMMain.cpp for the client game-logic module) and it is not designed to
be invoked directly (activating the executable by double-clicking on the
exe file in WindowsOS). The game-logic modules (client game and server
game) are created as child processes by the virtual machine (see
daemon/src/engine/framework/VirtualMachine.cpp) The main functions of
the modules calls
`static void CommonInit(Sys::OSHandle `*`rootsocket`*`)` and from within
this function the program enters its main (infinite) loop
(`while(true)`) and this function interfaces with the virtual machine
with the function
`void VM::VMHandleSyscall(uint32_t `*`id`*`, Util::Reader `*`reader`*`)`,
this function is contained within the sg_api.cpp (src/sgame/sg_api.cpp)
and cg_api.cpp (src/cgame/cg_api.cpp) files.

The sg_api.cpp file contains code that receives messages from its VM and
executes function callbacks depending on the type of message received.
The initialization related messages are:

`GAME_STATIC_INIT`:

1.`VM::InitializeProxies(`*`milliseconds`*`)` - invokes 2 other
initialization functions, `Cmd::InitializeProxy()` and
`Cvar::InitializeProxy()`, to register commands with the VM and to
register global static client variables (cvars).

2.`FS::Initialize()` - sends a message to the VM and the VM interfaces
with the engine to initialize the filesystem.

3.`VM::VMInit()` - makes the VM allocate memory for clients and game
entities and loads map collision data.

`GAME_INIT`:

1\. Sets `g_cheats.integer` to the parameter value of *`cheats`*

2\. `G_InitGame` - this function is called from sg_main.cpp and performs
many functions, such as setting the cvars inside the VM to default
values, and defines global level variables, and sets up logging, and
gets server info, and loads config files, and initializes entities for
the game, and loads emoticons, and etc. see `G_InitGame` of sg_main.cpp
at about line 690 for more details.

The init message codes are different for cg_api.cpp, `CG_STATIC_INIT`
and `CG_INIT`, the purpose of them both are the same, although there are
some minor differences. See cg_api.cpp for more information. The
`CG_INIT` message is generated by the engine and transmitted to the
client game-logic module for processing, the message originates from
src/engine/client/cl_cgame.cpp within the function
`void CGameVM::CGameInit(int serverMessageNum, int clientNum)`. There is
one initialization message unique to cg_api.cpp and that is
`CG_ROCKET_VM_INIT`.

`CG_ROCKET_VM_INIT`:

1\. `CG_Rocket_Init` - essentially starts the user interface for the
game, the user interface for the game is based on libRocket.

Some information related to the VM and program ignition, from a comment
in the file src/engine/framework/VirtualMachine.h:

`* To better support mods the gamelogic is treated like any other asset and can`
`* be downloaded from a server. However it is considered untrusted code so we`
`* need to run it in a sandbox. We use NaCl to provide the sandboxing which`
`* means that the gamelogic is in another process and that we have to use IPC and`
`* shared memory to communicate with it.`
`*`
`* The gamelogic can be compiled to and ran from several executable formats that`
`* will all start at the "main" function whose first job will be to retrieve the`
`* root socket handle to communicate with the engine. The different executable`
`* formats are:`
`*  - A native shared library loaded at runtime and started in the engine process,`
`* this shared lib exports a "main" function pointer which is called by the`
`* engine, providing a handle to the root socket in argv[1]. Because the gamelogic`
`* lives in the same process as the engine, any leaks in the gamelogic will be`
`* engine leaks. However because it is in the same process, it is easier to debug`
`* as the debugger doesn't automatically attach to child process.`
`*  - An NaCl executable started in a new sandboxed process. The "main" function is`
`* ran first and the root socket handle is given via an environment variable. This`
`* is how the gamelogic is ran when we do not trust the code as it won't be able to`
`* access anything apart from the file handles the engine gives it. When the NaCl`
`* gamelogic exits the OS will clean up any leaks for us. It is also slightly slower`
`* than native format (no SSE and code alignment constraints).`
`*  - A native executable started in a new process, obviously the "main" function`
`* is the first one ran. The root socket handle is given in argv[1]. It doesn't`
`* provide sandboxing like the nacl executable but the OS will still clean up any`
`* leak for us.`
`*`
`* When setting the cgame VM type to non-default values, make sure to use /devmap`
`* (rather than /map) as it is a 'CHEAT' cvar.`
`*`
`* TL;DR`
`* - Native DLL: no sandboxing, no cleaning up but debugger support. Use for dev.`
`* - NaCl exe: sandboxing, no leaks, slightly slower, hard to debug. Use for regular players.`
`* - Native exe: no sandboxing, no leaks, hard to debug. Might be used by server owners for perf.`

## Lag Compensation

Daemon uses Neil "haste" Toronto's [Unlagged
mod](https://www.ra.is/unlagged/contents.html).

## Data Files

Daemon uses a variety of file formats. Many of these formats are custom.

See [Formats](Formats "wikilink") for details.

- Bot behavior trees
- Player configuration files
  - Crosshair configuration
  - Pubkey
  - GUID
- Server configuration files
  - [Map layouts](Map_layouts "wikilink")
  - Map rotations
- Particle & trail system files
- Sound configurations
  - [Buildables](Music_and_sounds#Buildables "wikilink")
- Model data ([discussion of supported
  formats](Exporting_Models#What_is_MD5.3F "wikilink"))
  - Skins
  - [MD3 animation configuration
    files](Exporting_Models#MD3_3 "wikilink") — specify which frames are
    for which animations, [MD3](Formats_MD3 "wikilink") is now
    discouraged in favor of [IQM](Formats_IQM "wikilink").
  - Configuration files
    - [Buildables](Exporting_Models#Buildables_2 "wikilink")
    - [Weapons](Exporting_Models#Weapons_2 "wikilink")
    - [Player models](Exporting_Models#Player_models_2 "wikilink")
- Map data
  - Map geometry (BSPs)
  - Color grading configurations

## Game Logic

Game logic is split into twos areas: server-side, and client-side, user
interface is part of client side. Each runs in its own [virtual
machine](Virtual_machines "wikilink").

On Quake 3 derivatives like Tremulous, there was `cgame.qvm`, `game.qvm`
and `ui.qvm` (client-side, server-side, user interface).

With Dæmon Engine and Unvanquished there are `cgame.nexe` and
`sgame.nexe` (client-side and server-side).

**Game Logic Categories:** The game code can be thought of as being
separated into two distinct categories: game objects and gameplay.

**Game Objects or Entities:** Game objects are the objects that exist in
the game world, they have a graphical representation (the actual game
asset, such as the armory mesh model), they have hit points, and can
receive damage from a source and die if their hit points reaches 0, they
can heal themselves (replenish hit points), and they are created when
the map loads or while the game is running (for example when a player
creates a drill entity to increase build points for their team), and
they can be destroyed, and etc. Entities in Unvanquished are designed to
have components, a component is a C++ class with gameplay functionality
that is incorporated into the basic entity itself and the basic entity
acquires the functionality of the component. A component is owned by a
parent entity. The base class definition for Unvanquished game entities
is contained inside of Unvanquished/src/sgame/backend/CBSEBackend.h.

The base class for Unvanquished game entities is nested inside of the
base class for game entities of the original Quake III source, see
`struct gentity_s` at line 111 of Unvanquished/src/sgame/sg_struct.h.

Here are some example component classes:

`class ArmouryComponentBase` - at line 1867 of
Unvanquished/src/sgame/backend/CBSEBackend.h

`class HealthComponentBase` - at line 475 of
Unvanquished/src/sgame/backend/CBSEBackend.h

`class ThinkingComponentBase` - at line 359 of
Unvanquished/src/sgame/backend/CBSEBackend.h

There are a number of CBSE (and so Unvanquished) entity related helper
functions located in the file Unvanquished/src/sgame/Entities.h, and
their implementation inside the cpp file.

Client-local game entities are drawn as computer graphics on the
player's screen, any client input related interactions with these
entities are transmitted to the server as commands and the server
processes these commands and invokes the gameplay code for the entity or
entities.

There is an absolute maximum number of entities of 1024 (see
*MAX_GENTITIES* macro definition of
daemon/src/engine/qcommon/qshared.h), if this maximum is reached then
the server will terminate. All active game entities are listed inside a
global array (*g_entities*, see sg_main.cpp), when a new entity is
created the server searches this list for the next available free entity
slot and initializes this slot, the server may force an entity slot to
be reallocated to a new entity though this may lead to problems
according to a comment in the file sg_entities.cpp:

*Try to avoid reusing an entity that was recently freed, because it can
cause the client to think the entity morphed into something else instead
of being removed and recreated, which can cause interpolated angles and
bad trails.*

Clients are game entities too and from 0 to (*MAX_CLIENTS* - 1)(see
daemon/src/engine/qcommon/q_shared.h) of the server global game entity
array is reserved for client entities.

**CBSE:** Unvanquished uses the CBSE Toolchain to implement the game
entity components. CBSE is a code generator based on Python and requires
Python3 and Python3-yaml to generate the actual C++ code, and a C++ 11
compiler to compile the generated code. See
<https://github.com/DaemonEngine/CBSE-Toolchain> for more information.

**Gameplay:** Gameplay code is all the code that makes the entities do
things and defines game rules and defines game events and defines game
behaviors. There is a lot of code in this category and only a little
some of the code will be used as an example. Gameplay is server-local,
meaning gameplay effects happens on the server. For example, the combat
mechanics and behaviors of the game Unvanquished are defined in the file
src/sgame/sg_combat.cpp. When a player dies the function *G_PlayerDie*
is called and this function handles game events related to the death of
a player, such as adding credit to a client's score and broadcasting a
notification to the clients saying a player has died. Another example of
gameplay code is the player movement code, contained inside of the file
src/shared/bg_pmove.cpp. When a player moves their player character with
their keyboard that input is transmitted to the server as a client
command and the server calls the functions inside bg_pmove.cpp to apply
the movement change to the player character game entity in the game
level simulated by the game server, a client is changing the position
and orientation of their associated player character entity on the
server.

**Client-Local Game Logic:** Buildable information is encapsulated in
the `cg_buildables` array (declared in )

Constants used to define gamelogic variables are in .

Types:

- `buildableInfo_t` — Encapsulates data associated with buildables
  (sounds, animations, etc.).
- `buildable_t` — An enumeration of all buildable types.
- `buildableAttributes_t` — Encapsulates gameplay information associated
  with buildables. There is an array of these called `bg_buildableList`.

## sg_main.cpp

The file src/sgame/sg_main.cpp deserves its own section since there are
a lot of core server game functions and important variables inside this
file.

A special structure with server game level information is inside this
file, the `level_locals_t level` variable.

sg_main contains the proxy console variables, the game-logic modules
cannot access the console variables directly so they are accessed via a
proxy interface.

**Some Important Server Functions:**

- `G_InitGame` - this function initializes the server game
- `G_SpawnClients` - spawns the clients into the server game
- `G_RunFrame` - executes the server game frame
- `G_RunThink` - executes the thinking code of the server game entities
- `ExitLevel` - changes the server game level after the intermission

**The Game Frame:** The game frame is a single moment or instant of the
game. For the client, the game frame is a single render frame of the
game. Gameplay and game objects are processed on a frame basis, the game
is updated to the current frame and then presented to the player as an
immediate moment in the game. This is the purpose of the function
G_RunFrame, as in Game_RunFrame. This function does all ***game
updates*** for console variables, for game entities, and entity events,
and etc. See the function definition for G_RunFrame of sg_main.cpp for
implementation details.

## Particle & Trail System

See and .

For the syntax, please see the [Tremulous
documentation](https://dl.unvanquished.net/docs/20060317-000.tremulous-manual.pdf)
(it's the same).

## Renderer

Source code for the modern OpenGL renderer is located in . This is an
OpenGL 3.1 Core (and later) renderer providing backward compatibility
with OpenGL 2.1.

The renderer was sometime referred to as the “GL3” renderer in opposite
to the now-removed “legacy” renderer (also called “vanilla” in the past)
which was an OpenGL 1 renderer (inherited from Tremulous Quake 3).

Renderer is a new renderer initially wrote for the XreaL engine (a
parent of the Dæmon engine).

### Notes

- Shaders are implemented as subclasses of the `GLShader` class. All are
  defined in .
- Each GLSL shader has their compilation and loading controlled by the
  single `GLShaderManager` class
- Compiled shaders are cached to disk when possible to speed up load
  times
- Shader compilation may be done up front before the game loads, or
  delayed till the main menu depending on the value of `r_lazyShaders`
- All possible parameters (what OpenGL calls ["uniform
  variables"](http://www.opengl.org/sdk/docs/man4/xhtml/glUniform.xml))
  that may be passed to a shader are enumerated through multiple
  inheritance.
  For Example, `gl_genericShader` is of type `GLShader_generic` which
  derives from the following classes.
  That list may be obsolete, see `GLShader_generic` class definition in
  for up to date information:
  - `GLShader`
  - `u_ColorTextureMatrix`
  - `u_ViewOrigin`
  - `u_ViewUp`
  - `u_AlphaThreshold`
  - `u_ModelMatrix`
  - `u_ModelViewProjectionMatrix`
  - `u_ColorModulate`
  - `u_Color`
  - `u_Bones`
  - `u_VertexInterpolation`
  - `u_DepthScale`
  - `GLDeformStage`
  - `GLCompileMacro_USE_VERTEX_SKINNING`
  - `GLCompileMacro_USE_VERTEX_ANIMATION`
  - `GLCompileMacro_USE_VERTEX_SPRITE`
  - `GLCompileMacro_USE_TCGEN_ENVIRONMENT`
  - `GLCompileMacro_USE_TCGEN_LIGHTMAP`
  - `GLCompileMacro_USE_DEPTH_FADE`
  - `GLCompileMacro_USE_ALPHA_TESTING`

<!-- -->

- The `u_*` parent classes provide functions that allow external code to
  set shader uniforms. e.g
  `gl_genericShader->SetUniform_ColorTextureMatrix()`

<!-- -->

- GLSL shaders may be found in `src/engine/renderer/glsl_source`. Please
  see the [full article](GLSL_Shaders "wikilink") for a complete
  listing.

### Helper Classes

As mentioned above, shader classes make use of multiple inheritance to
give them the relevant methods for controlling their behavior.

#### Compile Macros

Compile macros are used to reduce the number of uniforms needed, and
speed up execution by eliminating useless `if ( )` statements.

They also allow for easy code reuse when turning off some features like
e.g Normal Mapping.

Compile macros are set when rendering before the call to
`shader->BindProgram()`.

This list may be obsolete, an updated list can be found in the
`EGLCompileMacro` enum definition in file:

- `GLCompileMacro_USE_BSP_SURFACE`
- `GLCompileMacro_USE_VERTEX_SKINNING`
- `GLCompileMacro_USE_VERTEX_ANIMATION`
- `GLCompileMacro_USE_VERTEX_SPRITE`
- `GLCompileMacro_USE_TCGEN_ENVIRONMENT`
- `GLCompileMacro_USE_TCGEN_LIGHTMAP`
- `GLCompileMacro_USE_LIGHT_MAPPING`
- `GLCompileMacro_USE_DELUXE_MAPPING`
- `GLCompileMacro_USE_HEIGHTMAP_IN_NORMALMAP`
- `GLCompileMacro_USE_RELIEF_MAPPING`
- `GLCompileMacro_USE_REFLECTIVE_SPECULAR`
- `GLCompileMacro_LIGHT_DIRECTIONAL`
- `GLCompileMacro_USE_SHADOWING`
- `GLCompileMacro_USE_DEPTH_FADE`
- `GLCompileMacro_USE_PHYSICAL_MAPPING`
- `GLCompileMacro_USE_ALPHA_TESTING`

### Resources

Mac OS X users with XCode installed can access OpenGL man pages via the
terminal.

Alternatively, OpenGL API reference documentation is available online:

- [OpenGL 3.3 Reference Pages](http://www.opengl.org/sdk/docs/man3/)
- [OpenGL Shading Language (GLSL) Reference
  Pages](http://www.opengl.org/sdk/docs/manglsl/)
- [OpenGL 3.3 & GLSL Quick Reference
  Card](http://www.khronos.org/files/opengl-quick-reference-card.pdf)

## Valgrind and OpenGL drivers

Some OpenGL drivers may cause Valgrind to spew out a lot of false
errors. You can suppress these by using the
`--suppressions=/path/to/file.supp` flag. You must pass the full path
(no use of the tilde symbol). For example, the following
[file](http://www.mediafire.com/?z6ehwrxpw2m469h) can be used as a
template for your suppression file when using the fglrx driver, keeping
in mind that the location of the fglrx library may need to be changed.
Note: the fglrx driver no longer exist, but the tip may apply to others
drivers.

## Resources

### Publications

- [Bungie, Inc.](http://halo.bungie.net/Inside/publications.aspx) —
  creators of the Marathon, Myth, and Halo franchises.
- [DICE SE](http://dice.se/publications/) — creators of the Battlefield
  franchise.
- [Guerilla Games](http://www.guerrilla-games.com/publications/) —
  creators of the Killzone franchise.
  Also of interest is the "Making of Killzone 2" video series, not
  listed on their site:

  - [Part
    1](http://www.ign.com/videos/2009/01/27/killzone-2-ps3-the-making-of-killzone-2-part-1?objectid=748475)
  - [Part
    2](http://www.ign.com/videos/2009/01/27/killzone-2-ps3-the-making-of-killzone-2-part-2?objectid=748475)
  - [Part
    3](http://www.ign.com/videos/2009/01/27/killzone-2-ps3-the-making-of-killzone-2-part-3?objectid=748475)
  - [Part
    4](http://www.ign.com/videos/2009/01/27/killzone-2-ps3-the-making-of-killzone-2-part-4?objectid=748475)
- [Valve
  Software](http://www.valvesoftware.com/company/publications.html) —
  creators of the Half-Life franchise.

### General Game Development

- [Devmaster.net](http://devmaster.net/)

### OpenGL

- [Official OpenGL page](http://www.opengl.org/)
- [OpenGL 3.3 Reference Pages](http://www.opengl.org/sdk/docs/man3/)
- [OpenGL Shading Language Reference
  Pages](http://www.opengl.org/sdk/docs/manglsl/)
- [Learning Modern 3D Graphics
  Programming](http://arcsynthesis.org/gltut/)

### Quake

- [John Carmack's notes from
  development](http://fd.fabiensanglard.net/doom3/pdfs/johnc-plan_1999.pdf)
- "Looking at the Quake 3 Source"
  - [Part
    1](http://element61.blogspot.com/2005/08/looking-at-quake-3-source-part-1.html)
  - [Part
    2](http://element61.blogspot.com/2005/08/looking-at-quake-3-source-part-2.html)
  - [Part
    3](http://element61.blogspot.com/2005/09/looking-at-quake-3-source-part-3.html)
- [Code3Arena](http://www.quakewiki.net/archives/code3arena/)
- [MD5 file format](http://www.modwiki.net/wiki/MD5_(file_format))
  (website down since 2013, use
  <https://web.archive.org/web/20120930061040/http://www.modwiki.net/wiki/MD5_%28file_format%29>
  )
- [Another MD5 format
  article](http://tfc.duke.free.fr/coding/md5-specs-en.html)
- [Quake 3 Source Code
  Review](http://fabiensanglard.net/quake3/index.php)
- [Quake3World Discussion
  Forums](http://www.quake3world.com/forum/index.php)
- [ioquake3 project wiki](http://wiki.ioquake3.org/) — Primarily
  oriented for users, developers and server administrators.