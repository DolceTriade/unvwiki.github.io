---
title: Optimisations
permalink: /Optimisations/
---

## In game options

## Open-source Radeon users (Linux)

The Open-Source Radeon driver enforces Vsync by default. On at least
Radeon 6790 cards the framerate is better (constant 60FPS without
tearing) with it turned off.

From the Arch Linux [wiki page on
radeon](https://wiki.archlinux.org/index.php/Radeon#Turn_vsync_off):

<div style="background-color: #CCCCCC; padding: 1em; margin: 1em;">

The radeon driver will enable vsync by default, which is perfectly fine
except for benchmarking. To turn it off, create ~/.drirc (or edit it if
it already exists) and add the following section:

    <driconf>
        <device screen="0" driver="dri2">
            <application name="Default">
                <option name="vblank_mode" value="0" />
            </application>
        </device>

    </driconf>

</div>

After editing/creating this file, restart X to complete the changes. For
most users this involves logging out and back in again.