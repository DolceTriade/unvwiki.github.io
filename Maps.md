---
title: Maps
permalink: /Maps/
---

## Map repositories

Places you can download DPKs or source repositories for various maps.

### Ready-to-play DPKs for Unvanquished

All of the URLs here are HTTP servers used to provide automatic
downloads when a player connects to a server but lacks a needed pak, so
they will have other kinds of paks besides maps. You can find these URLs
by setting `/logs.level.client.pakDownload debug` in the console and
connecting to a server while missing a pak, then looking for the console
line starting `Debug: Checking for PAKSERVER in`. The rest of the line
is the download base URL.

Excluding the "official" maps in the Unvanquished release, the vast
majority of available maps were originally made for Tremulous or other
games. The owners of servers mentioned here have generally done some
testing and touch-ups to ensure the maps work correctly in Unvanquished,
but not everything works 100%.

- Official maps: <https://dl.unvanquished.net/pkg/>
- Maps from the server "Map&Bot Testing EU" run by Sweet:
  <https://users.unvanquished.net/~sweet/pkg/>. 350 maps as of November
  2023.
- Maps from the server "deadbeef" run by bmorel:
  <http://deadbeef.fr/unvanquished/>. 313 maps as of November 2023. Has
  a directory with [levelshots](Levelshot "wikilink").

### Tremulous maps in original form (.pk3)

You can also find a bunch of maps from Tremulous:
[1](https://dl.unvanquished.net/mercenaries-guild/public_html/maps/).
Despite this link being on official's Unvanquished's server, those are
\*not\* officially supported and require modifications to be played. If
you are lucky, you can get them working (locally) by simply renaming
them in your own unvanquished/pkg folder like this: . And despite all
this, there is no guarantee those will work, and even less that they'll
be bug-free.

Feel free to meet us on [2](https://unvanquished.net/chat/) to ask what
needs to be done to have those more widely used by server owners!

### Source repositories

Git repositories with sources (.map files). For mappers and project
maintainers. Must be built with NetRadiant or Urcheon to be playable.

- Official maps are in the
  [UnvanquishedAssets](https://github.com/UnvanquishedAssets)
  organization on Github. The map `$mapname$` can be found at
  `https://github.com/UnvanquishedAssets/map-$mapname$_src.dpkdir`.
- [Interstellar
  Oasis](https://github.com/InterstellarOasis/InterstellarOasis) is a
  collection of "first-class" source ports by illwieckz of Tremulous
  maps. These are unofficial maps, but the work is done by one of the
  Unvanquished project heads.
- [Masmblr's Github](https://github.com/Masmblr?tab=repositories) has
  source repositories for 26 Tremulous maps created by himself.

## Official Unvanquished Maps

These maps are distributed with the default installation

<table>
<thead>
<tr class="header">
<th><p>Name and Description</p></th>
<th><p>Levelshot</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Antares</strong></p>
<ul>
<li>Varied rooms and corridors</li>
</ul>
<p>by Pevel</p></td>
<td><figure>
<img src="antares.jpg" title="antares.jpg" width="400" />
<figcaption>antares.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Chasm</strong></p>
<ul>
<li>Two route design</li>
<li>Medium sized</li>
<li>Outside area</li>
</ul>
<p>by Supertanker</p></td>
<td><figure>
<img src="Levelshots-Snowstation-b4.jpg"
title="Levelshots-Snowstation-b4.jpg" width="400" />
<figcaption>Levelshots-Snowstation-b4.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>Forlorn</strong></p>
<ul>
<li>Varied rooms and corridors</li>
</ul>
<p>by EmperorJack</p></td>
<td><figure>
<img src="Forlorn.jpg" title="Forlorn.jpg" width="400" />
<figcaption>Forlorn.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Parpax</strong></p>
<ul>
<li>Medium sized</li>
<li>Many branching paths</li>
<li>Crawl spaces and piping</li>
<li>Elevators</li>
</ul>
<p>by Viech</p></td>
<td><figure>
<img src="Levelshots-Parpax_compressed.jpg"
title="Levelshots-Parpax_compressed.jpg" width="400" />
<figcaption>Levelshots-Parpax_compressed.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>Perseus</strong></p>
<ul>
<li>Medium sized</li>
</ul>
<p>by Pevel</p></td>
<td><figure>
<img src="Perseus.jpg" title="Perseus.jpg" width="400" />
<figcaption>Perseus.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Platform 23</strong></p>
<ul>
<li>Symmetrical</li>
<li>Replacement for ATCS</li>
<li>Two route design</li>
</ul>
<p>by EmperorJack</p></td>
<td><figure>
<img src="Levelshots-Plat23-b11.jpg" title="Levelshots-Plat23-b11.jpg"
width="400" />
<figcaption>Levelshots-Plat23-b11.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>Spacetracks</strong></p>
<ul>
<li>Varied rooms, corridors and layers</li>
<li>Many Elevators</li>
<li>Crawl spaces</li>
</ul>
<p>by Supertanker</p></td>
<td><figure>
<img src="Levelshots-Spacetracks-r1.jpg"
title="Levelshots-Spacetracks-r1.jpg" width="400" />
<figcaption>Levelshots-Spacetracks-r1.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Station15</strong></p>
<ul>
<li>Varied rooms and corridors</li>
<li>Elevators</li>
</ul>
<p>by Supertanker</p></td>
<td><figure>
<img src="Levelshots-Station15-r1.jpg"
title="Levelshots-Station15-r1.jpg" width="400" />
<figcaption>Levelshots-Station15-r1.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>Thunder</strong></p>
<ul>
<li>Very large</li>
</ul>
<p>by EmperorJack</p></td>
<td><figure>
<img src="Levelshot-thunder.jpeg" title="Levelshot-thunder.jpeg"
width="400" />
<figcaption>Levelshot-thunder.jpeg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Vega</strong></p>
<ul>
<li>Large</li>
</ul>
<p>by Ingar</p></td>
<td><figure>
<img src="vega.jpg" title="vega.jpg" width="400" />
<figcaption>vega.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>Yocto</strong></p>
<ul>
<li>Vertical</li>
</ul>
<p>by Pevel</p></td>
<td><figure>
<img src="Levelshot-Yocto-b1a.jpg" title="Levelshot-Yocto-b1a.jpg"
width="400" />
<figcaption>Levelshot-Yocto-b1a.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
</tbody>
</table>

# Gentrified Maps

Maps that were born in Tremulous.

<table>
<thead>
<tr class="header">
<th><p>Name and Description</p></th>
<th><p>Levelshot</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>.:U.T:C.S:.</strong></p>
<ul>
<li>Symmetrical</li>
<li>Two route design</li>
<li>Small</li>
</ul></td>
<td><figure>
<img src="Levelshot-Utcs.jpg" title="Levelshot-Utcs.jpg" width="400" />
<figcaption>Levelshot-Utcs.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Arachnid 2</strong></p>
<ul>
<li>Varied rooms, corridors and layers</li>
<li>Crawl spaces and piping</li>
<li>Medium sized</li>
</ul></td>
<td><figure>
<img src="Levelshots-Arachnid2.jpg" title="Levelshots-Arachnid2.jpg"
width="400" />
<figcaption>Levelshots-Arachnid2.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>Beyond Derelict</strong></p>
<ul>
<li>Varied rooms, corridors and layers</li>
<li>Crawl spaces</li>
<li>Large</li>
</ul>
<p>by Danny "Megabite" Marcus</p></td>
<td><figure>
<img src="Levelshots-Derelict.jpg" title="Levelshots-Derelict.jpg"
width="400" />
<figcaption>Levelshots-Derelict.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Karith Station 2</strong></p>
<ul>
<li>Varied rooms, corridors and layers</li>
<li>Outside area</li>
<li>Crawl spaces</li>
<li>Large</li>
<li>Elevators</li>
</ul>
<p>by Godmil</p></td>
<td><figure>
<img src="Levelshots-Karith.jpg" title="Levelshots-Karith.jpg"
width="400" />
<figcaption>Levelshots-Karith.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>Meep</strong></p>
<ul>
<li>Varied rooms, corridors and layers</li>
<li>Crawl spaces</li>
<li>Medium sized</li>
</ul>
<p>By Catalyc</p></td>
<td><figure>
<img src="Levelshots-Meep.jpg" title="Levelshots-Meep.jpg"
width="400" />
<figcaption>Levelshots-Meep.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Methane (beta 1)</strong></p>
<ul>
<li>Large</li>
<li>Vertically complex</li>
</ul>
<p>by Ingar</p></td>
<td><figure>
<img src="Levelshots-Methane-beta1.jpg"
title="Levelshots-Methane-beta1.jpg" width="400" />
<figcaption>Levelshots-Methane-beta1.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>Nano!</strong></p>
<ul>
<li>Very Small</li>
<li>Symmetrical</li>
</ul>
<p>by Ingar</p></td>
<td><figure>
<img src="Levelshots-Nano.jpg" title="Levelshots-Nano.jpg"
width="400" />
<figcaption>Levelshots-Nano.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Nexus 6</strong></p>
<ul>
<li>Varied rooms, corridors and layers</li>
<li>Crawl spaces</li>
<li>Medium sized</li>
</ul></td>
<td><figure>
<img src="Levelshots-Nexus6.jpg" title="Levelshots-Nexus6.jpg"
width="400" />
<figcaption>Levelshots-Nexus6.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>Niveus : Outpost 652</strong></p>
<ul>
<li>Varied rooms, corridors and layers</li>
<li>Medium sized</li>
</ul></td>
<td><figure>
<img src="Levelshots-Niveus.jpg" title="Levelshots-Niveus.jpg"
width="400" />
<figcaption>Levelshots-Niveus.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Orion I - communication ship (beta 2)</strong></p>
<ul>
<li>Varied rooms, corridors and layers with some vents</li>
<li>Medium sized</li>
</ul>
<p>by Xenom[GER]</p></td>
<td><figure>
<img src="Levelshots-Orion.jpg" title="Levelshots-Orion.jpg"
width="400" />
<figcaption>Levelshots-Orion.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>Procyon -</strong></p>
<ul>
<li>Varied rooms, corridors and layers and vents</li>
<li>Large sized</li>
</ul>
<p>by Ingar</p></td>
<td><figure>
<img src="Levelshots-procyon.jpg" title="Levelshots-procyon.jpg"
width="400" />
<figcaption>Levelshots-procyon.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Sirius -</strong></p>
<ul>
<li>Varied rooms, corridors and layers</li>
<li>Large sized</li>
</ul>
<p>by Ingar</p></td>
<td><figure>
<img src="Levelshots-sirius.jpg" title="Levelshots-sirius.jpg"
width="400" />
<figcaption>Levelshots-sirius.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>Tremor</strong></p>
<ul>
<li>Medium sized</li>
<li>Large rooms and corridors</li>
<li>Crawl spaces (underground section)</li>
</ul>
<p>by Vedacon</p></td>
<td><figure>
<img src="Levelshots-Tremor.jpg" title="Levelshots-Tremor.jpg"
width="400" />
<figcaption>Levelshots-Tremor.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>Uranium124</strong></p>
<ul>
<li>Varied rooms, corridors and layers</li>
<li>Small sized</li>
</ul>
<p>by CoderNem</p></td>
<td><figure>
<img src="Levelshots-uranium124.jpg" title="Levelshots-uranium124.jpg"
width="400" />
<figcaption>Levelshots-uranium124.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>

## community maps

Maps produced (and not already listed) by the community which are known
to work for unvanquished, for both tremulous and unvanquished.

Licences of images is the same as the map itself, this will be updated
later. This section have lot of things to do, including adding author's
names, licencing informations, simple map descriptions, etc.

<table>
<thead>
<tr class="header">
<th><p>Name and Description</p></th>
<th><p>Levelshot</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>area3</strong></p></td>
<td><figure>
<img src="Levelshots-area3.jpg" title="Levelshots-area3.jpg"
width="400" />
<figcaption>Levelshots-area3.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>atcshd</strong></p></td>
<td><figure>
<img src="Levelshots-atcshd.jpg" title="Levelshots-atcshd.jpg"
width="400" />
<figcaption>Levelshots-atcshd.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>ctcs</strong></p></td>
<td><figure>
<img src="Levelshots-ctcs.jpg" title="Levelshots-ctcs.jpg"
width="400" />
<figcaption>Levelshots-ctcs.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>dretchstorm</strong></p></td>
<td><figure>
<img src="Levelshots-dretchstorm.jpg" title="Levelshots-dretchstorm.jpg"
width="400" />
<figcaption>Levelshots-dretchstorm.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>fortification</strong></p></td>
<td><figure>
<img src="Levelshots-fortification.jpg"
title="Levelshots-fortification.jpg" width="400" />
<figcaption>Levelshots-fortification.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>hamunaptra</strong></p></td>
<td><figure>
<img src="Levelshots-hamunaptra.png" title="Levelshots-hamunaptra.png"
width="400" />
<figcaption>Levelshots-hamunaptra.png</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>hangar28</strong></p></td>
<td><figure>
<img src="Levelshots-hangar28.jpg" title="Levelshots-hangar28.jpg"
width="400" />
<figcaption>Levelshots-hangar28.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>jota</strong></p></td>
<td><figure>
<img src="Levelshots-jota.jpg" title="Levelshots-jota.jpg"
width="400" />
<figcaption>Levelshots-jota.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>openfield</strong></p></td>
<td><figure>
<img src="Levelshots-openfield.jpg" title="Levelshots-openfield.jpg"
width="400" />
<figcaption>Levelshots-openfield.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>peorongateb3</strong></p></td>
<td><figure>
<img src="Levelshots-peorongateb3.jpg"
title="Levelshots-peorongateb3.jpg" width="400" />
<figcaption>Levelshots-peorongateb3.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>ptcs2</strong></p></td>
<td><figure>
<img src="Levelshots-ptcs2.jpg" title="Levelshots-ptcs2.jpg"
width="400" />
<figcaption>Levelshots-ptcs2.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>rsmse</strong></p></td>
<td><figure>
<img src="Levelshots-rsmse.jpg" title="Levelshots-rsmse.jpg"
width="400" />
<figcaption>Levelshots-rsmse.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>stahl</strong></p></td>
<td><figure>
<img src="Levelshots-stahl.jpg" title="Levelshots-stahl.jpg"
width="400" />
<figcaption>Levelshots-stahl.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>terminus</strong></p></td>
<td><figure>
<img src="Levelshots-terminus.jpg" title="Levelshots-terminus.jpg"
width="400" />
<figcaption>Levelshots-terminus.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>transit</strong></p></td>
<td><figure>
<img src="Levelshots-transit.jpg" title="Levelshots-transit.jpg"
width="400" />
<figcaption>Levelshots-transit.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>uncreation</strong></p></td>
<td><figure>
<img src="Levelshots-uncreation.jpg" title="Levelshots-uncreation.jpg"
width="400" />
<figcaption>Levelshots-uncreation.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td><p><strong>urbanp2</strong></p></td>
<td><figure>
<img src="Levelshots-urbanp2.jpg" title="Levelshots-urbanp2.jpg"
width="400" />
<figcaption>Levelshots-urbanp2.jpg</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p><strong>usstremor</strong></p></td>
<td><figure>
<img src="Levelshots-usstremor.jpg" title="Levelshots-usstremor.jpg"
width="400" />
<figcaption>Levelshots-usstremor.jpg</figcaption>
</figure></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>

[Category:Maps](Category:Maps "wikilink")