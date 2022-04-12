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

Source: [Lyra Project](https://www.unrealengine.com/marketplace/en-US/product/lyra)

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

So, let's get a bit more funky with it and replicate the Lyra project setup for unique loading screens.

Say if you want different maps or gamemodes etc. have different loading screen slots, or pretty much whatever you want.

Start of by opening your IDE by choice, like Rider or Visual Studio.

We'll need to create a new `UCLASS` inheriting from `UGameInstanceSubsystem` with a delegate to broadcast when the widget class changed, a `UPROPERTY` for our delegate and another `UPROPERTY` for the current UserWidget class in your project.

You can do so like this:

```cpp
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FLoadingScreenWidgetChangedDelegate, TSubclassOf<UUserWidget>, NewWidgetClass);

UCLASS()
class COMMONLOADINGSAMPLE_API UCommonLoadingSubsystem : public UGameInstanceSubsystem
{
	GENERATED_BODY()
	
public:
	UCommonLoadingSubsystem();
  
private:
	UPROPERTY(BlueprintAssignable, meta=(AllowPrivateAccess))
	FLoadingScreenWidgetChangedDelegate OnLoadingScreenWidgetChanged;

	UPROPERTY()
	TSubclassOf<UUserWidget> LoadingScreenWidgetClass;
	
};
```

Then we'll have to declare two public functions:

SetLoadingScreenContentWidget:

```cpp
	UFUNCTION(BlueprintCallable)
	void SetLoadingScreenContentWidget(TSubclassOf<UUserWidget> NewWidgetClass);
```

and GetLoadingScreenContentWidget:

```cpp
	UFUNCTION(BlueprintPure)
	TSubclassOf<UUserWidget> GetLoadingScreenContentWidget() const;
```

We'll then implement these functions to get and set out Widget Class, this class will be used to populate our Loading Screen widgets Named Slot component.

This is what Epic Games' implementation looks like in Lyra and is how I also implemented it in this example:

```cpp
void UCommonLoadingSubsystem::SetLoadingScreenContentWidget(TSubclassOf<UUserWidget> NewWidgetClass)
{
	if (LoadingScreenWidgetClass != NewWidgetClass)
	{
		LoadingScreenWidgetClass = NewWidgetClass;

		OnLoadingScreenWidgetChanged.Broadcast(LoadingScreenWidgetClass);
	}
}

TSubclassOf<UUserWidget> UCommonLoadingSubsystem::GetLoadingScreenContentWidget() const
{
	return LoadingScreenWidgetClass;
}
```

and this is it for the c++, not too bad. Go ahead and build your solution and we'll head back into the engine.

Let's start by creating our main loading screen widget, this will contain a Named Slot we can use to populate the unique loading screens with different content. This is what my implementation looks like:

<image>

I also made a default content widget that I keep in the Named Slot in-case we ever do a loading screen in a situation where that isn't set up.

Now, inside of our main loading screen userwidget blueprint graph let's get the UCommonLoadingSubsystem we made earlier and get the content class. Let's then populate the Named Slot with that widget. (Note: You'll likely want to implement some checks here, I have not in this case) 

<image2>

With that in place the last thing that remains is to implement setting the userwidget class of the content we want to display before entering into a loading screen. In this example I made a BP_Portal that will open a map when a player walks over it. You can see my example setup below:

<image3>

In this case the "Loading Class" variable is instance editable and set per actor in the world outliner.

After this is all set up you're done and should end with a result like this:

<video>

## Minigame loading screen
---

<insert>
