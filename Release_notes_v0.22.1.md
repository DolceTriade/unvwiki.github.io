---
title: Release notes v0.22.1
permalink: /Release_notes/v0.22.1/
---

# Major issues and workarounds

<table style="float:right;border-spacing:1em;">
<tr>
<td>

<figure>
<img src="V0.22.1_nocurses_winXP.png"
title="File:V0.22.1 nocurses winXP.png" />
<figcaption><a href="File:V0.22.1">File:V0.22.1</a> nocurses
winXP.png</figcaption>
</figure>

</td>
</tr>
</table>

<table>
<thead>
<tr class="header">
<th><p>Problem</p></th>
<th><p>Specific requirements</p></th>
<th><p>Solution</p></th>
<th><p>Developer Status</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Poor framerate and stuttering of keypresses.</p></td>
<td><p>Windows</p></td>
<td><p>Start the game with '+nocurses' added to the command line
options.</p>
<p>Right click your shortcut for the game and add '+nocurses' to do
this: see image on right.</p></td>
<td><p>Known problem, will be fixed</p></td>
</tr>
<tr class="even">
<td><p>Some settings in the menus do not function</p></td>
<td><p>None</p></td>
<td><p>Use console commands to change these options instead.</p>
<p>High quality settings example:</p>
<p><code>r_subdivisions 4</code><br />
<code>r_vertexlighting 0</code><br />
<code>r_picmip 0</code><br />
<code>r_inGameVideo 1</code><br />
<code>cg_shadows 4</code><br />
<code>r_dynamiclight 1</code><br />
<code>cg_bounceParticles 1;</code><br />
<code>r_normalMapping 1</code><br />
<code>r_bloom 1</code><br />
<code>r_rimlighting 1</code><br />
<code>cg_motionblur 0.05</code><br />
<code>r_ext_multisample 8</code><br />
<code>r_ext_texture_filter_anisotropic 8</code><br />
<code>r_heathaze 1</code><br />
<code>r_texturemode GL_LINEAR_MIPMAP_LINEAR</code></p></td>
<td><p>Known problem, will be fixed</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

# Minor Issues

<table>
<thead>
<tr class="header">
<th><p>Problem</p></th>
<th><p>Specific requirements</p></th>
<th><p>Solution</p></th>
<th><p>Developer Status</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>r_picmip (texture quality setting) does not affect the quality of
<em>all</em> textures</p></td>
<td><p>None</p></td>
<td><p>No workaround</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Basilisk grab is not unlagged</p></td>
<td><p>None</p></td>
<td><p>Aim ahead of moving enemies to grab them</p></td>
<td><p>Developers are going to redesign basilisk gameplay anyway
</p></td>
</tr>
<tr class="odd">
<td><p>Bots get stuck</p></td>
<td><p>None</p></td>
<td><p>Play on bot-friendly maps without fiddly sections — such as <a
href="Maps" title="wikilink">Platform 23</a> — and push bots out of
areas they get stuck in.</p></td>
<td><p>Bots are under heavy development and are always
changing.</p></td>
</tr>
<tr class="even">
<td><p>Keys get 'stuck' on</p></td>
<td><p>Low framerate/lag</p></td>
<td><p>Tap the 'stuck' key again to unstick it</p></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>