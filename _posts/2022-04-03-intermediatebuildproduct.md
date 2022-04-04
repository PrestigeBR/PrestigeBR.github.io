---
title: Blueprint Nodes are lying to you
tags: [Unreal Engine]
style: fill
color: secondary
description: Blueprint nodes in Unreal are lying to you, sometimes. Let's take a small peek under the hood to learn more...
---

{% include elements/figure.html image="https://docs.unrealengine.com/4.27/Images/ProgrammingAndScripting/Blueprints/UserGuide/FlowControl/DoOnce_Network.png" caption="Unreal Engine Blueprint Graph" %}

## Kismet Nodes

Unreal Engines Blueprint Graph uses something known as Kismet 2 Nodes or K2 Nodes for short.

They are the normal blueprint nodes that we all know and love from the engine but for the sake of this blog post I'll be referring to them as "K2 Nodes".

To explain to you why these nodes sometimes "lie" to you I'll have to explain some different types of K2 Nodes in Unreal.
They're both technically just K2Nodes and there are many different ways to make them but I'll be covering the two most common types you'll be running into when making them or in plugins and referring to them as "Intermediate nodes" and "Function nodes" in this blog post.

I won't be going too into depth so anyone can follow along.

I'll also cover how you can visualize your compiled blueprint graphs in-engine to help with debugging either your blueprints or your custom K2Nodes at the end of this post.

### Function nodes

Usually when I hear people explain what "Blueprint Nodes" are, it goes along the lines of 
>they're just blocks of c++ code in a visual format

and well, that is true, they are but it gets a bit more complicated than that.

One of the most common type of blueprint nodes you'll be working with are of the class `K2Node_CallFunction` which does what the name suggests, it calls a c++ function. 
This is the node class any of your `UFUNCTION` macros will be generating when exposing functions to Blueprints if you've ever exposed c++ logic to the engine before. This is pretty straight forward and makes sense with the aforementioned statement however not all nodes work like this.

### Intermediate nodes

Let's use the Format Text node as an example here:
{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/960628644420653086/unknown.png" caption="Uncompiled Blueprint FormatText" %}

What does it actually do? Let's take a look at the compiled blueprint logic here:
{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/960630332225380472/unknown.png" caption="Compiled Blueprint FormatText" %}

Let's start by explaining what is going on here...

The K2Node when compiled is executing logic that spawns "Intermediate" nodes, basically temporary nodes that are replacing your existing blueprint node with new ones that execute the actual logic.

This is the most common type of K2Node you'll find in plugins or make for yourself, these work pretty much exactly like a Blueprint Macro [(like explained here)](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/Blueprints/BestPractices/) does as well.

Here is another example from a ForEachMapLoop node I made for my [utility plugin](https://utils.hideout.no/):
{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/960632434792222720/unknown.png" caption="Custom For Each Map Loop" %}

There are more ways to make K2Nodes but these are the most common you'll need to understand when working with and making custom nodes for the engine.

Now, I won't go into depth on how to create K2Nodes in this post but if you're interessted in that check out this well written introduction from [MagForceSeven](https://www.gamedev.net/tutorials/programming/engines-and-middleware/improving-ue4-blueprint-usability-with-custom-nodes-r5694/).

>How does this help me?

Well, with this knowledge you can use it to optimize your blueprints or perhaps troubleshoot your own K2Nodes with this nifty trick I'll cover below and it should give you a pretty good baseline of how the most common type of K2Nodes you'll be making work.

### Visualize the Intermediate Build Product

You can show the compiled intermediate build product in your Blueprint Graph by enabling an option under:

 File -> Developer -> Save Intermediate Build Product
 
{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/960633894254809188/unknown.png" caption="Setting Location" %}

Then compile your blueprint graph and you'll see the intermediate graphs under "My Blueprints":

{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/960635209756323950/unknown.png" caption="Compiled Graphs" %}

and thats pretty much it. Thanks for reading, I hope you learned something!

Thanks to [Sebastian Krause](https://twitter.com/HatiEth) for showing me this useful trick.
