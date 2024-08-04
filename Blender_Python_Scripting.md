---
title: Blender Python Scripting
permalink: /Blender_Python_Scripting/
---

## Cookbook

### Print a list of vertex group names for the selected mesh

`for group in bpy.context.active_object.vertex_groups: print(group.name)`

### Print a list of bone names for the selected armature

`for bone in bpy.context.active_object.pose.bones: print(bone.name)`

## Frequently asked quesitons

### Blender 2.5

- *Question*: How can I write output to the console or to the info
  window?
  *Answer*: You can't write output to the info window or the console
  that appears in blender itself, but you can write to the system
  console. You can also create popups. You can probably also write to a
  text datablock. (fixme: write how to do this).