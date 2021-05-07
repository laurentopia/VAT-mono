VAT (Vertex Animation Texture) is a way to store animation by encoding vertex delta per frame as pixel value in a texture.
This is the Mono version of @maxartz15 Vertex Animation repo. It has only one dependency: URP 8.31

# TECH ART OUTSOURCE - Vertex Animation

![](Documentation~/Images/ProjectCastle_01.gif)

A vertex animation baking tool, shaders, and animation system for Unity DOTS/ECS.  
Render tens of thousands of models at the same time each with its own animation state.  

## Features

- Vertex animation model baker
  - Multiple animations (stored in one Texture2DArray)
  - LOD generation
  - Prefab generation
  - Animation book generation
- DOTS animation system
  - Simple API
  - Animation library and books
- Shaders
  - Lit vertex animation shader
  - Interpolation
  - Normal encoding and decoding
  - Shader graph support
  - Animation blending

### Model Baker

Artist friendly GUI for converting models.

![](Documentation~/Images/VA_ModelBaker_01.png)

### DOTS Animation System

Sample code to play an animation.

```C#
protected override void OnUpdate()
{
    float deltaTime = UnityEngine.Time.deltaTime;

    Entities.ForEach((Entity entity, ref VA_AnimatorComponent ac) =>
    {
        // Get the animation lib data.
        ref VA_AnimationLibraryData animationsRef = ref ac.animationLibrary.Value;

        // Set the animation index on the AnimatorComponent to play this animation.
        ac.animationIndex = VA_AnimationLibraryUtils.GetAnimation(ref animationsRef, animationName);

        // 'Play' the actual animation.
        ac.animationTime += deltaTime * animationsRef.animations[ac.animationIndex].frameTime;
    }).ScheduleParallel();
}
```

### Shaders

Lit example shader (build in shader graph).  
Full shader graph support.

![](Documentation~/Images/VA_Shaders_01.png)

## Install

[Installing from a Git URL](https://docs.unity3d.com/Manual/upm-ui-giturl.html)

[Documentation](Documentation~/VertexAnimation.md)

## Getting Started

- Example 1: Mainly used for testing.
- Example 2: Contains an animation system that shows how you could setup animated characters and a spawning system to test performance.
- Example 3: MonoBehaviour example for if you are not using DOTS.

## Used By

- [Project Castle](https://store.steampowered.com/app/1517150/Project_Castle/)

## LICENSE

Overall package is licensed under [MIT](/LICENSE.md), unless otherwise noted in the [3rd party licenses](/THIRD%20PARTY%20NOTICES.md) file and/or source code.
