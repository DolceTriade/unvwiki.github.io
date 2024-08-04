---
title: Virtual machines
permalink: /Virtual_machines/
---

The , following its inheritance from [Quake
3](http://www.fabiensanglard.net/quake3/qvm.php) is using two [virtual
machines](http://en.wikipedia.org/wiki/Virtual_machine) for server-side
game logic (src/gamelogic/game) and client-side game logic
(src/gamelogic/cgame). But unlike Quake 3, there is no virtual machine,
the user interface is implemented in the client-side gamelogic.

Note that even when playing alone, the server VM is still used; it is
just run locally in the same executable instead of in the dedicated
server game executable on another machine.

Communication between virtual machines and the engine is done with calls
to "trap" functions. These functions have the "trap_" prefix:

<table>
<thead>
<tr class="header">
<th><p>Virtual Machine</p></th>
<th><p>API implementation</p></th>
<th><p>API header</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Server-side gamelogic</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Client-side gamelogic</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>