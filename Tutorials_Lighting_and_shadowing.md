---
title: Tutorials Lighting and shadowing
permalink: /Tutorials/Lighting_and_shadowing/
---

In modeling, you may have noticed how shading can appear not quite as
you would expect. A common mistake is to assume that changing the
shading of a face from smooth to flat or vice-versa will affect the
finished model in-game: this is false. To understand why this is so and
why models are shaded the way they are in-game, you must first
understand vertex and face normals and their role in lighting
calculations. Once this is understood, the problem can be mitigated most
easily with the EdgeSplit modifier. An example of how this may be useful
is shown below:

<table>
<tbody>
<tr class="odd">
<td><figure>
<img src="normals_explained_edgesplit_on.png"
title="normals_explained_edgesplit_on.png" />
<figcaption>normals_explained_edgesplit_on.png</figcaption>
</figure></td>
<td><figure>
<img src="normals_explained_edgesplit_off.png"
title="normals_explained_edgesplit_off.png" />
<figcaption>normals_explained_edgesplit_off.png</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p>EdgeSplit on</p></td>
<td><p>EdgeSplit off</p></td>
</tr>
</tbody>
</table>

As you can see, the EdgeSplit modifier makes quite a difference, but
before its use is explained, we must first explain the role of normals
in lighting. The normal of a polygon is the vector that is used to
determine how light should be reflected off a surface. A proper normal
vector is perpendicular to the surface. However, most graphics APIs
allow for arbitrary normal vectors; they may point in any direction. For
realistic lighting, the vector used for this purpose is perpendicular to
the polygon (obtained by the cross product of any two vectors coplanar
with the polygon, which for convenience are usually the sides) because
that is how lighting works in the real world.

<figure>
<img src="Normal_light_calculation_01.png"
title="Normal_light_calculation_01.png" />
<figcaption>Normal_light_calculation_01.png</figcaption>
</figure>

The above image shows the side view of a polygon (black) with a light
ray (red) reflecting off of it. The angle the light ray travels in as it
reflects off of the polygon is the same relative to the normal (blue) as
it was before it reflected.

It was said before that normals are typically calculated as being
perpendicular to a polygon. However, in practice, graphics APIs use
Gouraud shading, which concerns itself not with one normal vector for an
entire polygon but rather a normal at each vertex of that polygon. The
normal used at any point on the face is actually the interpolation of
the vertex normals. This would be useless if vertex normals were always
perpendicular to the polygon as the interpolation would always then also
be perpendicular. Instead, the normal vectors at each vertex are not
necessarily perpendicular to the polygon. Rather, when using smooth
shading in Blender, the vertex normals are calculated as the average of
the normals of every face that shares that vertex. A simple example is
shown below:

<table>
<tbody>
<tr class="odd">
<td><figure>
<img src="Normals_explained_face_normals.png"
title="Normals_explained_face_normals.png" />
<figcaption>Normals_explained_face_normals.png</figcaption>
</figure></td>
<td><figure>
<img src="Normals_explained_vertex_normals.png"
title="Normals_explained_vertex_normals.png" />
<figcaption>Normals_explained_vertex_normals.png</figcaption>
</figure></td>
</tr>
<tr class="even">
<td><p>Face normals</p></td>
<td><p>Vertex normals</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
</tr>
</tbody>
</table>

Note that in both of these images, the polygons on the right have
EdgeSplit applied to an edge, shown in a light blue color.

This is where EdgeSplit comes in. Marking an edge sharp causes EdgeSplit
to effectively ignore the face normals of the polygons on the other side
of a sharp edge when calculating the vertex normals at that edge, so
instead of one vertex normal that is the average of every face normal at
that vertex, multiple normals are used depending on the face.

[Category:Tutorials](Category:Tutorials "wikilink")
[Category:Modeling](Category:Modeling "wikilink")