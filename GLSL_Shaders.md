---
title: GLSL Shaders
permalink: /GLSL_Shaders/
---

# Uniform Variables

As described in the [technical
documentation](Technical_Documentation "wikilink"), all possible
parameters (what OpenGL calls ["uniform
variables"](http://www.opengl.org/sdk/docs/man4/xhtml/glUniform.xml))
that may be passed to a shader are enumerated in the `shaderProgram_t`
structure in
[`src/engine/rendererGL/tr_local.h:1359`](https://github.com/Unvanquished/Unvanquished/blob/master/src/engine/rendererGL/tr_local.h).

<table>
<thead>
<tr class="header">
<th><p>Type</p></th>
<th><p>Name</p></th>
<th><p>Used by</p></th>
<th><p>Set with</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ColorMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_CurrentMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ContrastMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_DiffuseMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_NormalMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_SpecularMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_LightMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_DeluxeMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_DepthMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_DepthMapBack</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_DepthMapFront</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_PortalMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_AttenuationMapXY</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_AttenuationMapZ</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ShadowMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ShadowMap0</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ShadowMap1</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ShadowMap2</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ShadowMap3</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ShadowMap4</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_EnvironmentMap0</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_EnvironmentMap1</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_RandomMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_GrainMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_VignetteMap</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ColorTextureMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_ColorTextureMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_DiffuseTextureMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_DiffuseTextureMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_NormalTextureMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_NormalTextureMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_SpecularTextureMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_SpecularTextureMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_AlphaTest</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>alphaTest_t</code></p></td>
<td><p><code>t_AlphaTest</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ViewOrigin</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>vec3_t</code></p></td>
<td><p><code>t_ViewOrigin</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>GLint</code></p></td>
<td><p><code>u_DeformParms</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_Color</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>vec4_t</code></p></td>
<td><p><code>t_Color</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ColorModulate</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>vec4_t</code></p></td>
<td><p><code>t_ColorModulate</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_AmbientColor</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>vec3_t</code></p></td>
<td><p><code>t_AmbientColor</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_LightDir</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>vec3_t</code></p></td>
<td><p><code>t_LightDir</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_LightOrigin</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>vec3_t</code></p></td>
<td><p><code>t_LightOrigin</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_LightColor</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>vec3_t</code></p></td>
<td><p><code>t_LightColor</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_LightRadius</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_LightRadius</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_LightParallel</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>qboolean</code></p></td>
<td><p><code>t_LightParallel</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_LightScale</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_LightScale</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_LightWrapAround</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_LightWrapAround</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_LightAttenuationMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_LightAttenuationMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_LightFrustum</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ShadowMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_ShadowMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ShadowCompare</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>qboolean</code></p></td>
<td><p><code>t_ShadowCompare</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ShadowTexelSize</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>float</code></p></td>
<td><p><code>t_ShadowTexelSize</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ShadowBlur</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>float</code></p></td>
<td><p><code>t_ShadowBlur</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>GLint</code></p></td>
<td><p><code>u_ShadowParallelSplitDistances</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>vec4_t</code></p></td>
<td><p><code>t_ShadowParallelSplitDistances</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_RefractionIndex</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>float</code></p></td>
<td><p><code>t_RefractionIndex</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_FresnelPower</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_FresnelScale</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_FresnelBias</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_NormalScale</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_EtaRatio</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_FogDensity</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_FogColor</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_FogDistanceVector</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>vec4_t</code></p></td>
<td><p><code>t_FogDistanceVector</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_FogDepthVector</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>vec4_t</code></p></td>
<td><p><code>t_FogDepthVector</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_FogEyeT</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_FogEyeT</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_SSAOJitter</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_SSAORadius</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_ParallaxMapping</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>qboolean</code></p></td>
<td><p><code>t_ParallaxMapping</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_DepthScale</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_DepthScale</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_PortalClipping</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>qboolean</code></p></td>
<td><p><code>t_PortalClipping</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_PortalPlane</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>vec4_t</code></p></td>
<td><p><code>t_PortalPlane</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_PortalRange</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_PortalRange</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_EnvironmentInterpolation</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_EnvironmentInterpolation</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_HDRKey</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_HDRKey</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_HDRAverageLuminance</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_HDRAverageLuminance</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_HDRMaxLuminance</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_HDRMaxLuminance</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_DeformMagnitude</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_DeformMagnitude</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ModelMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_ModelMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ViewMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_ViewMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ModelViewMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_ModelViewMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ModelViewMatrixTranspose</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_ModelViewMatrixTranspose</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ProjectionMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_ProjectionMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ProjectionMatrixTranspose</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_ProjectionMatrixTranspose</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_ModelViewProjectionMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_ModelViewProjectionMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_UnprojectMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>matrix_t</code></p></td>
<td><p><code>t_UnprojectMatrix</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_VertexSkinning</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>qboolean</code></p></td>
<td><p><code>t_VertexSkinning</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>GLint</code></p></td>
<td><p><code>u_VertexInterpolation</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>float</code></p></td>
<td><p><code>t_VertexInterpolation</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_BoneMatrix</code></p></td>
<td><p>vertexSkinning_vp.glsl:</p>
<ul>
<li><code>VertexSkinning_P_N</code></li>
<li><code>VertexSkinning_P_TBN</code></li>
</ul></td>
<td><p><code>u_BoneMatrix::SetUniform_BoneMatrix()</code></p></td>
</tr>
<tr class="even">
<td><p><code>int32_t</code></p></td>
<td><p><code>u_Time</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>float</code></p></td>
<td><p><code>t_Time</code></p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

# Shaders

## blurX_fp.glsl

## blurX_vp.glsl

## blurY_fp.glsl

## blurY_vp.glsl

## cameraEffects_fp.glsl

## cameraEffects_vp.glsl

## computeLight_fp.glsl

Provide reusable functions for computing light effects (like
specularity).

## contrast_fp.glsl

## contrast_vp.glsl

## debugShadowMap_fp.glsl

## debugShadowMap_vp.glsl

## deformVertexes_vp.glsl

## depthtile1_fp.glsl

Part of the tiled renderer.

## depthtile1_vp.glsl

Part of the tiled renderer.

## depthtile2_fp.glsl

Part of the tiled renderer.

## depthtile2_vp.glsl

Part of the tiled renderer.

## dispersion_C_fp.glsl

## dispersion_C_vp.glsl

## fogGlobal_fp.glsl

## fogGlobal_vp.glsl

## fogQuake3_fp.glsl

## fogQuake3_vp.glsl

## forwardLighting_fp.glsl

## forwardLighting_vp.glsl

## fxaa3_11_fp.glsl

Provides `FxaaPixelShader` function we use in fxaa_fp.glsl

## fxaa_fp.glsl

FXAA code.

## fxaa_vp.glsl

FXAA code.

## generic_fp.glsl

## generic_vp.glsl

## heatHaze_fp.glsl

## heatHaze_vp.glsl

## lightMapping_fp.glsl

## lightMapping_vp.glsl

## lighttile_fp.glsl

Part of the tiled renderer.

## lighttile_vp.glsl

Part of the tiled renderer.

## liquid_fp.glsl

## liquid_vp.glsl

## motionblur_fp.glsl

## motionblur_vp.glsl

## portal_fp.glsl

## portal_vp.glsl

## reflection_CB_fp.glsl

## reflection_CB_vp.glsl

## refraction_C_fp.glsl

## refraction_C_vp.glsl

## reliefMapping_fp.glsl

Provide reusable functions to process normal and height maps.

## screen_fp.glsl

## screen_vp.glsl

## shadowFill_fp.glsl

## shadowFill_vp.glsl

## skybox_fp.glsl

## skybox_vp.glsl

## ssao_fp.glsl

## ssao_vp.glsl

## vertexAnimation_vp.glsl

Contains vertex shaders to perform skinning for skeletal meshes (MD5
models).

### Uniform Variables

- `int` u_VertexSkinning
- `mat4` u_BoneMatrix\[MAX_GLSL_BONES\]

### Attributes

- `vec4` attr_BoneIndexes —
- `vec4` attr_BoneWeights —

### VertexSkinning_P_N

Translates a vertex and corresponding vertex normal as per the bone
matrices (as many as the `MAX_GLSL_BONES` preprocessor constant allows)
contained in the uniform variable `u_BoneMatrix`, which is set with the
`u_BoneMatrix::SetUniform_BoneMatrix()` method.

Returns `void`.

#### Arguments

- `const vec4` inPosition — The position of the skinned mesh vertex in
  3d space that will be transformed by the `u_BoneMatrix` matrices.
- `const vec3` inNormal— The normal vector (for lighting calculations)
  corresponding to the `inPosition` vertex that will be transformed by
  the `u_BoneMatrix` matrices.
- `inout vec4` position — The transformed vertex.
- `inout vec3` normal — The transformed normal.

### VertexSkinning_P_TBN

Returns `void`.

#### Arguments

- `const vec4` inPosition
- `const vec3` inTangent
- `const vec3` inBinormal
- `const vec3` inNormal
- `inout vec4` position
- `inout vec3` tangent
- `inout vec3` binormal
- `inout vec3` normal

## vertexSimple_vp.glsl

## vertexSkinning_vp.glsl

## vertexSprite_vp.glsl

## volumetricFog_fp.glsl

## volumetricFog_vp.glsl