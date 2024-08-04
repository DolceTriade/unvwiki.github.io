---
title: Formats Image
permalink: /Formats/Image/
---

The terms <dfn>lossy</dfn> and <dfn>lossless</dfn> are used multiple
times in this page. Lossy means that images compressed using that format
will lose some of their image quality to save space. Lossless means that
the compression will not sacrifice image quality, no matter how much you
compress the image with that format.

See also , and .

## Tools

See [Tools/Image](Tools_Image "wikilink").

## Licensing

The following licenses are suitable for images:

## Supported formats

The engine supports the following formats:

- [CRN](https://github.com/DaemonEngine/crunch) — A compressed lossy
  texture format similar to DDS (see below) but more efficient.
  to store lossy assets (except skyboxes for some technical reasons).
- [WebP](https://developers.google.com/speed/webp/) — A relatively new
  format created by Google that provides excellent lossy compression
  (generally 39% smaller filesize than an equivalent JPEG) and lossless
  compression (better than PNG).
  as lossless variant to store lossless assets (lightmaps,
  deluxemaps).
  as lossy variant to store skyboxes.
- [DDS (DirectDraw
  Surface)](http://www.modwiki.net/wiki/DDS_%28file_format%29) — A
  container format by Microsoft to store
  [S3TC](http://en.wikipedia.org/wiki/S3_Texture_Compression) compressed
  textures, which is natively supported by video cards without needing
  any prior decompression, ensuring short loading times.
  .
- [KTX (Khronos Texture)](https://www.khronos.org/ktx/) — another
  GPU-compressed format.
  .
- [PNG (Portable Network Graphics)](http://www.libpng.org/pub/png/) —
  Provides lossless compression of images, but with the penalty of high
  filesize.
  , .
- TGA — Lossless format usually used uncompressed (some TGA format
  variant support compression but not all tools may support them).
  Usually found uncompressed in legacy Tremulous assets.
  , .
- JPEG — Provides lossy compression and very small filesizes, but image
  quality can suffer at higher compression values. Usually found in
  legacy Tremulous assets.
  , .

## Recommended formats in repositories

It's recommended to store data files in well-known lossless formats in
data repositories.

Convert TGA or lossless Webp to PNG to store them in repositories. It's
better to compress to specific formats (CRN, WebP) while you distribute
your work for use in game, but please keep them lossless and in
widely-used formats in repositories!

If your original file is already in JPEG format or lossy WebP, store it
as is without recompressing it to something else.

Because CRN, KTX or DDS may not be easy to edit, you may want to convert
them back to lossless PNG anyway to make to make them easy to edit. You
may otherwise prefer to just store them as is to prevent further lossy
recompression. Official Unvanquished data repositories will not accept
CRN, KTX or DDS files.

It is good to store 's `.xcf` source in repositories. Because Git is not
for big large heavy weighty files, please tick the compression option
when saving from GIMP (if you don't have this option, your version of
GIMP is old, please update!), then save as `.xcf.xz` to get even more
compression (or compress the `.xcf` file with `xz` before committing).

## Recommended formats

## Targeting the OpenGL3 renderer

Creating textures for use with the modern OpenGL3 renderer of the is
slightly different than texture creation for the renderer of the old
Quake 3 engine you may know. This is not due to changes in formats or
the like, but because of how additional rendering technologies change
what information is to be encoded in which textures. Each successive
rendering technology removes further information from your base texture,
until only albedo (diffuse) remains:

<table>
<thead>
<tr class="header">
<th><p>Technology</p></th>
<th><p>Texture</p></th>
<th><p>Base texture</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Diffuse mapping</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Height mapping</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Normal mapping</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Specular mapping</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Physical mapping</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>Glow mapping</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

Note: specular maps and physical maps are mutually exclusives, they are
different techniques to fit the same need. Physical maps are meant to be
more realistic than specular ones.

## Packing conventions

<figure>
<img src="DaemonEngineTexturePacking.png"
title="Image:DaemonEngineTexturePacking.png" />
<figcaption>Image:DaemonEngineTexturePacking.png</figcaption>
</figure>

See this document:
<https://dl.unvanquished.net/docs/20210506-001.daemon-engine-texture-packing.pdf>

## Naming conventions

## Material creation

See .

## Resources

- [id Software guide to creating specular maps (web
  archive)](https://web.archive.org/web/20160321000904/https://www.iddevnet.com/quake4/ArtReference_SpecularMaps)

[Category:Formats](Category:Formats "wikilink")
[Category:Texturing](Category:Texturing "wikilink")
[Category:Modeling](Category:Modeling "wikilink")
[Category:Mapping](Category:Mapping "wikilink")