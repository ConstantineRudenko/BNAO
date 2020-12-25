# [--> Successor/cousin repository](https://github.com/Fewes/BakerBoy)

# BNAO
![alt text](https://raw.githubusercontent.com/Fewes/BNAO/master/Example.png)
![alt text](https://raw.githubusercontent.com/Fewes/BNAO/master/UI.png)

# Features
* Supports baking ambient occlusion or bent normal maps from low-poly geometry, right in the editor.
* Supports baking with alpha-tested materials.
* Bakes textures for selected objects and automatically groups meshes into same output textures based on material usage (with option for overriding grouping).
* Can bake tangent, object and world-space bent normal maps.
* Automatically uses normal maps present in original materials for a higher quality result.
* Can bake objects with or without occlusion from other scene objects.
* Can convert normal maps from tangent to object space and vice-versa.

# Requirements
BNAO runs on regular (as in, not compute) shaders and thus does not demand much from your GPU. However, it does require support for floating point and shadow map format render textures. To check if this is supported on your platform, use these functions:  
SystemInfo.SupportsRenderTextureFormat(RenderTextureFormat.ARGBFloat);  
SystemInfo.SupportsRenderTextureFormat(RenderTextureFormat.Shadowmap);  

# What are bent normals?
![alt text](https://raw.githubusercontent.com/Fewes/BNAO/master/BentNormalsExample.gif)  
Bent normal maps store the direction of least occlusion (in other words, the direction in which the most ambient light is coming from) in a texture.  
They can be used to occlude cubemap reflections based on the view direction in a much more realistic way than just multiplying with an ambient occlusion term. They can also be used to get an ambient color value which more closesly resembles a ray traced result.  
For details on how to implement these effects in your own shader, see the file "Shader Implementation Example.txt".

# Can I specify a max distance for the ambient occlusion?
No. The baker uses depth textures (similar to shadow mapping) to determine ray intersections, which makes it impossible to bias the result based on distance.

# The normals convertor outputs weird results!
Make sure your texture settings for the input texture are correct. For TS normals just set "Texture Type" to "Normal Map". For OS normals, leave it at "Default" but uncheck "sRGB (Color Texture)".
