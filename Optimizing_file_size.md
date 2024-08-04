---
title: Optimizing file size
permalink: /Optimizing_file_size/
---

Those are tricks that can be used to save file space in released
archives, packages and repositories.

## Binaries

Extracting debug files from binaries means the binary is smaller in
memory and faster to extract from the archive storing it. (For example
if a mod ships some file, the symbols can be saved in another file using
a better compression algorithm (for example, ) in the same zip the files
are, given the engine will never have to load the symbols it will both
save file space, game memory usage, and binary extraction time.

## Images

### XCF

XCF files to be stored in repositories can be compressed to xz. GIMP
knows how to open and save files.

One can simply write file extension in the GIMP saving dialog when
saving the file, or compress with tool an existing uncompressed file.

This compression is better than the builtin compression checkbox
available in the save dialog GIMP (the builtin one is believed to use
zlib and is less efficient). Also, files can just be decompressed with
the tool to load them in third-party tools that may not support .

### PNG

PNG images can be compressed further by removing some metadata (like
metadata telling what tool produced it), and some tools like can be used
to recompress the PNG using the best PNG storage profile. The PNG
efficency doesn't really come from the compression algorithm (it is not
better than zip), but comes from the various storage profiles and the
way to code or not code RGB, palettes, alpha channels…

The tool uses a genetic algorithm to find filter combinations that
produces file that compresses well.

Then, the internal zlib compression can be optimized using the *Zopfli*
algorithm, like when using the tool which adds zopfli-optimized zlib
compression over the storage optimization of . The tool also supports
zopfli but is not as optimal as .

Since those tools keep the original file if they fail to compress more,
and sometime one can do better than the other, it is a good idea to
first strip the PNG from useless metadata, then re compress the PNG with
then recompress it with to produce the smallest possible files.

Existing TGA files better be compressed into optimized PNG before saving
them in repositories.

### JPG

A tool similar to zopfli exists for files, it is named but there is no
reason to use it.

The reason why there is no reason to use zopfli is that JPEG is already
a lossy format, so recompressing a JPG to a JPG would just degrade more
the image while keeping other JPG limitations.

Lossy JPG are recommended to be recompressed to CRN format as well (as
CRN is better for GPU memory usage, so since we recommend converting JPG
to CRN when recompressing JPG to another lossy format, there is no
reason to convert JPG to JPG.

For lossless images like PNG or TGA that have to be recompressed into a
lossy format, prefer compressing into the CRN format instead of JPG.

So we don't have usage for guetzli for the game. It may have some usage
for some web resources though.

### CRN

For CRN normal maps without height maps, better use the option that
shifts some channels to make lossy compression more efficient. This
option reuses the alpha channel for non-alpha data (destructing the
alpha channel in the process) that's why the option must only be used
with normal maps without height map in alpha channel. For normal maps
with height map in alpha channel, the standard crunch compression should
be used instead.

Recent GIMP versions offer an option to compress some internal data. The
GIMP's files can be compressed with as files. Both compressions can be
done to get smaller files.

## Models

Blender supports a compressed variant that is just a file compressed
with to produce a file renamed as again.

## Zip

It's possible to store files in zip without storing the parent
directories, this save zip file space for a negligible cost. This would
mean directories permissions and change date will not be stored but
that's usually useless.

It's possible to set all the files to the same date, time and
permission. This will probably not reduce the zip file size itself, but
it will reduce the zip file size containing the zip file. So, for
example, setting all the files to the same date, time and permission
when creating a archive and an engine zip will reduce the size of the
release zip containing all of them.

The best zip compressor that is 7zip in zip mode, produces good result,
it's possible to achive more compression by increasing other options
like . By default is equivalent to .

It's possible to then produce smaller zip using zopfli-enable
compressors like . It's still a good idea to compress with 7zip before
compressing with advzip because 7z is really efficient and may stometime
produce smaller files than zopfli, so advzip will just keep the smallest
compression for each file.

To recompress a zip with advzip and zopfli, one can do , unfortunately
advzip processes every file in the archive sequentially. One may want to
compress every file in a separate zip, optimize every zip then produce
the final zip with .