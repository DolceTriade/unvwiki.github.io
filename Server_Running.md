---
title: Server Running
permalink: /Server/Running/
---

Servers can be quickly setup over LAN by starting a match in-game,
however this is not as powerful or efficient as running a dedicated
server separately.

# Netiquette

Servers may be needed in some geographical places to reduce ping delay.

# Getting the server

Our standard [download](https://unvanquished.net/download/) contains the
server. The binary is named .

To install on an headless server, you may prefer to download the
[universal zip](https://unvanquished.net/download/zip), example with
Linux:

`wget --content-disposition `[`https://unvanquished.net/download/zip`](https://unvanquished.net/download/zip)
`unzip unvanquished_``.zip`
`cd unvanquished_`
`unzip linux-amd64.zip`

# Starting the Server

Just running with a map may be enough:

    ./daemonded +map plat23

You always need to start a map (here, this is done by passing the
argument).

## Network configuration

By default the server listening port is , it is an port. You may have to
open this port in your firewall or redirect it to the machine running
the server.

This is the same port as Quake Ⅲ Arena, so other games derivated from
the Quake Ⅲ engine may share the same port and while the engine selects
the next port available if the default one is already taken, you may
want to enforce a port number if you host multiple games or game servers
to avoid the port for each server to change according to the server
start order.

# Advanced starting

You may want to customize the way it runs, for example change the
listening port (here for both IPv4 and IPv6, is the default port):

    ./daemonded -set net_port 27960 -set net_port6 27960 +map plat23

Or store the unvanquished server configuration in a specific folder:

    ./daemonded -homepath home/ +map plat23

Or tell the game server to also look for files you're distributing on
your web server:

    ./daemonded -pakpath /var/www/pkg +map plat23

## Server configuration

A ready-to use server configuration template can be found on folder of
Unvanquished repository.

You just need to copy the and folders into your user game directory.

You may want to edit the file to change some things like the server name
or things like that.

After that, you can run the server this way:

    ./daemonded +exec server.cfg

You can set arbitrary ports and run the configuration this way:

    ./daemonded -set net_port 27960 -set net_port6 27960 +exec server.cfg

## Options ordering

You can combine those options, but every starting with a must precede
every starting with a .

## Quick list of useful options

- — enabled ncurses console interface (default behavior is to disable it
  so messages remain on-screen after crashes).

- and — customize the default port, by default is is .

- — load more files from another directory.

- — without a map the server will kill itself.

## Directories

If installing from the universal zip, the default directory where the
are stored is in relative to the extraction directory.

An optional package directory is called a *pakpath*. Additional custom
paths can be added using the option. You can add as many as you want.

The default user directory is called the *homepath*. It can be
customized with the option.

The executable (*daemon dedicated*) should be included with your
installation.

So, if you need to be explicit on every path, you can do something like
that:

    ./daemonded -homepath ${HOME}/.local/share/unvanquished \
     -pakpath /var/www/unvanquished/pkg

### Standard game locations

See [Game locations](Game_locations "wikilink") for details.

## Script tutorial

Here is a tutorial to make a server script : [Server/Script
tutorial](Server_Script_tutorial "wikilink").

# Configuration and Operation

To discover more commands than are listed here, you can type the
command, and to discover configuration variables, you can type the
command.

There is command and cvar completion, you can type a first letter (eg
'g') and press **Tab** to list available options starting with that
letter.

If you are in a terminal: **Shift+Page Up** allows you to scroll and the
opposite for down.

You can also search in what is *already printed* using grep, for
example:

    /listCmds
    /grep map

## Server Config File

Here is the template for the server config: .

The `config` folder is stored in the `homepath` folder (see above).

For example on Linux it would be:
`${HOME}/.local/share/unvanquished/config`.

Ensure your server mode is not set to '2' unless you want your server to
be listed for other players.

`# Server mode`
`# 0 - local server`
`# 1 - LAN server`
`# 2 - public server`

Public servers will want to set sv_hostname to a non-default value

## Map rotation and map layouts

- [Map rotation](Server_Map_rotation "wikilink") — to customize the map
  loading order and on which condition a map is loaded or not.
- [Map layouts](Server_Map_layouts "wikilink") — default building
  locations.

## Commands

| Command     | Description                                                                               |
|-------------|-------------------------------------------------------------------------------------------|
| devmap      | Loads a map with `sv_cheats` enabled. `sv_cheats` cannot otherwise be changed during play |
| listadmins  | List current admins in-game                                                               |
| listlayouts | List available layouts (for this map?)                                                    |
| listplayers | List current players in-game                                                              |
| listmaps    | List maps available to the server                                                         |
|             |                                                                                           |

## Cvars

| Cvar             | Description                                                  |
|------------------|--------------------------------------------------------------|
| g_dretchPunt     | Allow dretches to be pushes out of the way by bigger aliens? |
| g_friendlyfire   | Allows players to hurt their team                            |
| g_gravity        | Gravity.                                                     |
| sv_maxclients    | Maximum number of players on the server                      |
| g_maxGameClients | Maximum number of players in teams (ignoring spectators)     |
| g_motd           | Message displayed to joining players (Message Of The Day)    |
| g_password       | Password to enter game                                       |
|                  |                                                              |

# Game administration

## Become admin

To make yourself an in-game admin

1.  Enter the game make sure you've set your in-game name (otherwise set
    it in the player settings)
2.  In the console, (<Shift><Escape> or the key below the escape key)
    use `/register`, it should say your account is now registered.
3.  Using `/listplayers`, find your player number (if you want to use
    your player number for use `/setlevel`)
4.  Finaly, go into an admin console (you may want to launch the game
    manually) and `/setlevel (your number/your nickname) (your level)`

It is also possible to modify the file ./game/admin.dat but the server
will require a reboot to take the change into account.

Here are the levels:

`[level]`
`level   = 5`
`name    = ^1Server Operator`
`flags   = ALLFLAGS -IMMUTABLE -INCOGNITO`

`[level]`
`level   = 4`
`name    = ^3Senior Admin`
`flags   = listplayers admintest adminhelp time putteam spec999 warn kick mute showbans ban namelog buildlog ADMINCHAT register unregister l0 l1`

`[level]`
`level   = 3`
`name    = ^2Junior Admin`
`flags   = listplayers admintest adminhelp time putteam spec999 warn kick mute ADMINCHAT buildlog register unregister l0 l1 `
` `
`[level]`
`level   = 2`
`name    = ^6Team Manager`
`flags   = listplayers admintest adminhelp time putteam spec999 register unregister`

`[level]`
`level   = 1`
`name    = ^5Server Regular`
`flags   = listplayers admintest adminhelp time register unregister`

`[level]`
`level   = 0`
`name    = ^4Unknown Player`
`flags   = listplayers admintest adminhelp time register`

[Category:Server](Category:Server "wikilink")
[Category:Tutorials](Category:Tutorials "wikilink")