---
title: Testing Models
permalink: /Testing/Models/
---

You may test models one of two ways: either by using the gameplay code
to cause that model to appear (i.e., by playing the game), or by
commanding the game to load an arbitrary model.

## Using `testmodel`

The `testmodel` command accepts a single parameter, which is the path to
the model that you would like to test. Provided that it can locate the
model, it will spawn it 100 units in front of whichever direction you
are currently facing.

## Using `testgun`

The `testgun` command will replace the currently held weapon with the
requested model. The model may be positioned on screen as follows:

- `cg_gunX` — The x-position of the weapon. The positive x-axis extends
  away from the view.
- `cg_gunY` — The y-position of the weapon. The positive y-axis extends
  to the left.
- `cg_gunZ` — The z-position of the weapon. The positive z-axis extends
  upward.

The model will not be animated, but the current frame of animation may
be controlled with `nextframe` and `prevframe`.

Weapon skins may be tested using `nextskin` and `prevskin`.

## Testing with gameplay code

- If the model is a buildable, weapon, or player model that is not
  immediately available (i.e., not available until you reached a certain
  amount of momentum), you can change the momentum stage with .
- If you do not have sufficient credits to purchase an item model you
  wish to test, or evos to evolve to the desired class, you may give
  yourself the maximum amount that you can carry with `/give all`.

## Tips

- To visually inpsect a model's bounding box, which is set by its
  configuration file, set `cg_drawBBox` to 1.
- To visually inspect the bone structure of a MD5 model, set
  `r_showSkeleton` to 1. *Note: at present there is a bug that causes
  bones to be displayed incorrectly. See [Issue
  \#2](https://github.com/Unvanquished/Unvanquished/issues/2) on GitHub
  for more information.*
- To hide map geometry, set `r_drawworld` to `0`. Note that with this
  set to `0`, PVS will still be in effect, so it might still be
  difficult to view your model.

[Category:Testing](Category:Testing "wikilink")
[Category:Modeling](Category:Modeling "wikilink")