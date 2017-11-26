# ShaderLab cheatsheet

## Intro
Shaders in Unity are written in custom "ShaderLab" declarative language. Actual shader code is written in Microsoft's HLSL.

Since I don't write shaders frequently, I usually forget all keywords, macros, etc. This document is not a guide or exhaustive documentation. Instead, it provides list of all basic functionally, and often used tricks for quick reference.

If you find that some information is missing or misleading, feel free to make pull request to [github repo](https://github.com/dario-zubovic/UnityShadersCheatsheet/).

## Table of contents
- [Structure](#structure)
- [Resources](#resources)
	- [Properties](#properties)

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
}
```

### Properties

## Resources

test
```HLSL

#pragma surface surf Standard fullforwardshadows vertex:vert

struct Input {
	float2 uv_MainTex;
};
```
