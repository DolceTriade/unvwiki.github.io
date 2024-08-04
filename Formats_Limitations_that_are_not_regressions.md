---
title: Formats Limitations that are not regressions
permalink: /Formats/Limitations_that_are_not_regressions/
---

Those are not regressions neither bugs but feature requests.

See also the [Known regressions since
Tremulous](Formats_Known_regressions_since_Tremulous "wikilink") page
for things that are regressions.

## Legacy features being only supported with legacy formats

### misc_anim_model only working with md3

=

The entities are currently only playing animations with legacy format.
The md3 format was using frame-based animation and newer formats like or
are using skeletal-based animations.

Since legacy Quake3 and Tremulous format is working as it worked before,
there is no regression.

Making entities play animation with skeletal formats is a feature
request.

## Experimental features that were never used

### liquidMap water code

The feature to render water surface with reflections and refraction is
not working.

Some very old screenshot proves it may have worked in the past, maybe
with unmerged code, and with unmerged data. It's also possible that the
code was in the legacy renderer that is now dropped since 10 years.

Making it working is a feature request.

## Experimental features there is no proof it ever worked (not a regression)

### func_door_model experimental Tremulous feature

The entities did not existed in Quake 3 code and is an experimental
feature of Tremulous. Editors like GtkRadiant and NetRadiant never
supported it and will not display the entity. An analysis of 1220 maps
from index shown none of them used that feature. It is unknown if that
feature was ever finished one day and if it has worked once. Bugs
affecting or it not working cannot be considered a regression.

Making it working is a feature request.

[Category:Formats](Category:Formats "wikilink")