---
title: Server Script tutorial
permalink: /Server/Script_tutorial/
---

Here is a tutorial to make a server script.

This tutorial makes the choice to create a custom `homepath` stored in
the same folder of unvanquished. It makes the tutorial easier, and it
makes easy for you to use a different `homepath` when you play and when
you host a server.

# Linux

Download the latest update by running this command in a folder of your
choice:

    wget --content-disposition https://unvanquished.net/download/zip

Extract this archive using this command:

`unzip unvanquished_``.zip`

Enter the unvanquished folder using this command:

`cd unvanquished_`

Extract the engine archive:

`unzip linux-amd64.zip`

Create a script to ease starting a server, create the file and give it
proper permissions:

`touch startsrv`
`chmod +x startsrv`

Write the script content this way:

`echo './daemonded -homepath home +exec server.cfg' > startsrv`

Create a folder called *home* in the unvanquished folder using this
command:

`mkdir home`

Create a folder called *config* in the *home* folder using this command:

`mkdir home/config`

Download the sample file using this command:

    wget -O home/config/server.cfg https://github.com/Unvanquished/Unvanquished/raw/master/dist/configs/config/server.cfg

Create a folder called *game* in the *home* folder using this command:

`mkdir home/game`

Download the sample file using this command:

    wget -O home/game/maprotation.cfg https://github.com/Unvanquished/Unvanquished/raw/master/dist/configs/game/maprotation.cfg

Edit the files to match your preferences if you need to, then quit:

`vim home/config/server.cfg`

`vim home/game/maprotation.cfg`

Run the server with:

`./startsrv`

# macOS

It's the same as Linux except this command to extract the engine
archive:

`unzip macos-amd64.zip`

And this command to write the script content:

`echo 'Unvanquished.app/Contents/MacOS/daemonded -homepath home +exec server.cfg' > startsrv`

# Windows

Download the latest version of Unvanquished from the GitHub releases
page [here](https://github.com/Unvanquished/Unvanquished/releases).

Extract the archive, open the extracted unvanquished folder.

Extract the `windows-amd64.zip` engine archive, if it create a folder
named `windows-amd64`, move the content of `windows-amd64` into the
unvanquished folder and delete the now empty `windows-amd64` folder.

Open the notepad text editor and paste this content:

`@daemonded.exe -homepath home +exec server.cfg`

Then save this file as `startsrv.cmd` in the unvanquished folder (make
sure it is named `startsrv.cmd` and not `startsrv.cmd.txt`).

Create a folder named *home* in the unvanquished folder.

Create a folder named *config* in the *home* folder and download the
sample file in that *config* folder folder.

Create a folder named *game* in the *home* folder and download the
sample file in that *game* folder.

Edit those files to match your preferences if you need to.

Run the server by double-clicking the `startsrv.cmd` file icon.

[Category:Server](Category:Server "wikilink")