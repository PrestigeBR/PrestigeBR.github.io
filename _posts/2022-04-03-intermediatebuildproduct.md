---
title: Blueprint Nodes are lying to you (sometimes)
tags: [Unreal Engine]
style: fill
color: secondary
description: Blueprint nodes in Unreal Engine aren't always what they say they are. Click to read more...
---

{% include elements/figure.html image="https://docs.unrealengine.com/4.27/Images/ProgrammingAndScripting/Blueprints/UserGuide/FlowControl/DoOnce_Network.png" caption="Unreal Engine Blueprint Graph" %}

## Kismet Nodes

Unreal Engines Blueprint Graph uses something known as Kismet 2 Nodes or K2 Nodes for short.
They are the normal blueprint nodes that we all know and love from the engine.

To explain to you why these nodes sometimes "lie" to you I'll have to explain two different types of K2 Nodes in Unreal.
They're both technically just K2Nodes and there are different ways to make K2Nodes but I'll be covering the two most common types you'll run into and referring to them as "Intermediate nodes" and "Function nodes" in this blog post.

### Function nodes

Usually when I hear people explain what "Blueprint Nodes" are, it goes along the lines of 
>they're just blocks of c++ code in a visual format
and well, they are but it gets a bit more complicated than that.

A lot, if not most blueprint nodes are of the class `K2Node_CallFunction` which does what the name suggests, it calls a c++ function like you'd expect. 
This is the type of node that any of your `UFUNCTION` macros will be creating when exposing functions to Blueprints if you've ever exposed c++ logic to the engine before. This is pretty straight forward and makes sense with the aforementioned statement however this brings me into

### Intermediate nodes

When you use a `Switch` node in the Blueprint graph you might expect it to be a regular plain old Switch statement going on, well... spoiler alert: it's not.

Normally you'd expect a Switch statement to look something like this:
```cpp
switch(expression) {
  case x:
    // code block
    break;
  case y:
    // code block
    break;
  default:
    // code block
}
```

but, the `K2Node_Switch` looks something like this:
-put image or code-

Now, I won't go into depth how this works or how to create K2Nodes here but if you're interessted in that check out this well written introduction from (MagForceSeven)[https://www.gamedev.net/tutorials/programming/engines-and-middleware/improving-ue4-blueprint-usability-with-custom-nodes-r5694/].

So, let's start by explaining what is going on here... -insert explanation-

### Visualize the Intermediate Build Product

-show how to save and visualize the intermediate build product-