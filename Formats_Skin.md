---
title: Formats Skin
permalink: /Formats/Skin/
---

A skin is used to display a [model](Formats_Model "wikilink") with
different textures than it was originally loaded with. Skin files
conventionally have the suffix `.skin`.

## Usage in Unvanquished

Skins are used with [player
models](https://github.com/UnvanquishedAssets/res-players_src.dpkdir/tree/master/models/players/%7Chuman)
to swap armors or add the helmet.

## Minimal .skin example

` foo,`<texture name>

For a model that has only a single texture, this skin file can be used
to replace it with a different one. `foo` is an arbitrary word that has
no effect. <texture name> should be replaced with the name of the
desired [Q3 shader](Formats_Material "wikilink") or an image path.

## Source code keywords

- Engine: `skin_t`
- Gamelogic: `trap_R_RegisterSkin`
- Both: `customSkin` (`refEntity_t` member)