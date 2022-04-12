---
title: "Loading Screens, the Epic way."
tags: [Unreal Engine]
description: "Let's take a look at the CommonLoadingScreen plugin used in Epic's Lyra content example. Click to read more..."
image: "https://cdn.discordapp.com/attachments/959186212046909551/963449212144586772/loadingscreens.png"
---

<!-- Intro Image -->

{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/963449212144586772/loadingscreens.png" caption="Written by André Valand" %}

<!-- Blog Post Content -->

## Introduction
---

Unreal Engine 5 had its production ready release recently, it came together with the new Lyra sample project from Epic Games containing a lot of goodies. 

In this blog post we'll be taking a look at the *CommonLoadingScreen* plugin in specific and I'll run you through how to set it up and use it in your own projects, trust me it is incredibly easy.

We'll be going through:
>  Plugin installation & basic setup<br>
>  Setting up unique loading screens based on context<br>
>  Modifying the plugin to allow for input so you can make loading screen minigames

## Installation
---

The CommonLoadingScreen plugin is not natively included in UE5 and is a Lyra project native plugin, so this is where we'll have to extract it from. You can choose to just copy over the plugin source, this is what I'll be doing so we can modify the source code slightly later, or you can package it and install it to your engine version if you want. Though I should note that by default there are some issues you'll have to clear up manually if you attempt to package the plugin such as giving BlueprintCallable functions categories and possibly shortening folder or class names because it's likely to go over the 260 character limit.

You can find the plugin in `LyraStarterProject/Plugins/CommonLoadingScreens`, proceed to copy this over into your own `<MyProjectName>/Plugins` folder and thats pretty much it for the setup outside the engine if you only want a basic loading screen.

## Basic setup
---

Upon loading up the engine, head to "Project Settings" and you'll find "CommonLoadingScreens" under the "Game" category. In here you'll be granted with a set of options, most of which are pretty self-explanatory or have tooltips explaining what they do.

{% include elements/figure.html image="https://cdn.discordapp.com/attachments/959186212046909551/963467358196875294/unknown.png" caption="Plugin Settings" %}
  
The main option you need to worry about here is the "Loading Screen Widget", this will be your base widget UserWidget class.
  
You can just set this option to be your widget of choice and you now have a functioning loading screen.

## Unique loading screens
---

<insert>

Link markdown: [google](https://google.com/)
