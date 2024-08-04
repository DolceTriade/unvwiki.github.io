---
title: UI LibRocket bugs
permalink: /UI/LibRocket_bugs/
---

- <s>r_gamma does not affect UI</s> Not desired. When I use r_gamma to
  compensate for an overly dark map I don't want it to fuck up the UI.
- <s>borders are shady. Sometimes they simply don't appear</s> Not
  seeing this as of 2023
- <s>objects 'jiggle' around when their class (eg :hover activated)
  changes, even though their size should not change.</s> Not seeing this
  of 2023
- <s>causes wincing pain</s> Sounds like a you problem

Sound:

- <s>sound loops from the last game keep playing in the loadscreen</s>
  Not seeing this as of 2023

Internal:

- rocketDebug does not work for HUD \<-
  <https://github.com/Unvanquished/Unvanquished/pull/1845> is an
  abandoned effort to get the debugger working again
- ui_restart causes crashes \<- I guess the modern equivalent is
  reloadHud? Needs testing

<select> Drop-down menus:

- large lists can go off-screen
- <s>misinterpret mouse coords (sometimes) and highlight/select the
  wrong entry</s> Not seeing this of 2023

Game start:

- <s>Errors in RML/CSS cause silent failures -\> crash (sometimes)</s>
  Not seeing this as of 2023

Match start:

- various HUD files are 'flashed' for a frame \[fixed\] \<- despite this
  being labeled \[fixed\] long ago, I recently fixed an instance of this
  in 2023 (c4dd3db81). Still not sure if all cases are fixed

Match load:

- <s>mouse cursor visible and locked to top-left corner</s> We just did
  a bunch of work on ensuring the right kind of cursor is displayed at
  the right time. Should be fixed

[Category:UI](Category:UI "wikilink")