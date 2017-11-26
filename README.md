# ShaderLab cheatsheet

## Intro
Shaders in Unity are written in custom "ShaderLab" declarative language. Actual shader code is written in Microsoft's HLSL.

Since I don't write shaders frequently, I usually forget all keywords, macros, etc. This document is not a guide or exhaustive documentation. Instead, it provides list of all basic functionally, and often used tricks for quick reference.

If you find that some information is missing or misleading, feel free to make pull request to [GitHub repo](https://github.com/dario-zubovic/UnityShadersCheatsheet/).

## Table of contents
- [Structure](#structure)
	- [Properties](#properties)
	- [SubShaders](#subshaders)
	- [Fallback](#fallback)
	- [CustomEditor](#customeditor)
- [Resources](#resources)

## Structure
```ShaderLab
Shader "Path/Name" {
	Properties {
		// properties visible in inspector and accessable through shader code
	}
	SubShader {
		// tags
		// passes	
	}
	Fallback "Fallback name"
	CustomEditor "editor name"
}
```

### Properties
```ShaderLab
[Attribute] _Name ("display name", Type) = Initial value
```

Name is usually given as \_CamelCase, but it's not required. Properties can be later accessed in as `[_Name]`.

**Types with proper initialization:**
- `_Name ("float value", Range(min, max)) = 0.5` - float, half, fixed (drawn as slider between `min` and `max` in inspector)
- `_Name ("float value", Float) = 0.5` - float, half, fixed
- `_Name ("integer value", Int) = 3` - int
- `_Name ("2D texture", 2D) = white {}` - sampler2D
- `_Name ("3D texture", 3D) = white {}` - sampler3D
- `_Name ("Cubemap", Cube) = white {}` - samplerCube
- `_Name ("Vector4", Vector) = (0, 0, 0, 0)` - float4, half4, fixed4
- `_Name ("sRGB color", Color) = (0, 0, 0, 0)` - float4, half4, fixed4 - converted to correct color space (drawn as color input field (color picker))

**Attributes:**
- `[HideInInspector]`
- `[NoScaleOffset]` - hide texture scaling / offset
- `[Normal]` - texture is normal map
- `[HDR]` - HDR texture
- `[Gamma]` - convert Float or Vector to correct color space
- `[PerRendererData]`

### SubShaders
There can be multiple subshaders provided per each shader. First one that can run on user's hardware is selected from the top towards the bottom. If multiple subshaders share commands, you can group them in one `Category {}` block with those commands provided once on the top.

Inside of `SubShader {}` block is "meat" of the shader, so that's what most of this cheatsheet will focus on.

### Fallback
If none of the provided SubShaders can run on user's hardware, Unity will try to use subshaders from different shader. You can use `Fallback Off` to disable this behaviour. No warning will be printed in case User's hardware doesn't supports any SubShaders.

### CustomEditor
Name of class that [extends ShaderGUI](https://docs.unity3d.com/Manual/SL-CustomShaderGUI.html) and will be used for drawing this shader's properties instead of default material inspector.

## Resources

test
```HLSL

#pragma surface surf Standard fullforwardshadows vertex:vert

struct Input {
	float2 uv_MainTex;
};
```
