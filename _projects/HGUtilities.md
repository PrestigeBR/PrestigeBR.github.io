---
name: HGUtilities
tools: [Unreal Engine, Plugin]
image: https://cdn.discordapp.com/attachments/959186212046909551/960641884714311680/unknown.png
description: Utility plugin(s) for Unreal Engine, includes 45+ extra nodes and latent actions in blueprint.
---

# [Extra Nodes](https://utils.hideout.no/)
---

A set of extra utility nodes for Blueprints in Unreal Engine.

I felt there was a lot of Blueprint functionality that was missing in Unreal Engine by default and made a plugin to speed-up my blueprint workflow.

## Custom K2Nodes

**PrintAny**

Print out any wildcard variable of types: ´Bool, Int, Byte, Float, Vector, Transform, Object, LinearColor, Name, Vector2D, Rotator and String´

{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/964281315052646451/unknown.png" caption="Blueprint Node" %}

Source: [Header](https://github.com/PrestigeBR/HGUtilNodes/blob/main/Source/CustomK2/Public/K2Node_PrintAny.h), [Implementation](https://github.com/PrestigeBR/HGUtilNodes/blob/main/Source/CustomK2/Private/K2Node_PrintAny.cpp)

**ForEachMapLoop**

Loop through any Blueprint Map variable and output per-index Index, Key & Value.

{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/964281209444270131/unknown.png" caption="Blueprint Node" %}

Source: [Header](https://github.com/PrestigeBR/HGUtilNodes/blob/main/Source/CustomK2/Public/K2Node_ForEachMapLoop.h), [Implementation](https://github.com/PrestigeBR/HGUtilNodes/blob/main/Source/CustomK2/Private/K2Node_ForEachMapLoop.cpp)

## Latent Actions

Run latent actions in Blueprint without the need for c++, this is only intended for prototyping because it has more overhead.

{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/964282559456485416/unknown.png" caption="Blueprint Nodes" %}

{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/964282918556016680/unknown.png" caption="Example Latent Action" %}

## Other nodes

This plugin overall has 45+ nodes. For a full list of nodes view the [documentation](https://utils.hideout.no/).

Some of the included nodes:

{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/964283755579723866/unknown.png" caption="Node Showcase" %}

View the [repository](https://github.com/PrestigeBR/HGUtilNodes).
