---
name: AINodeGraph
tools: [C++, AI, School]
image: https://cdn.discordapp.com/attachments/875515865540472842/1040541446643646474/AINodeGraphCover.png
description: This is a simple AI State/Task machine system and an accompanying node graph editor for runtime scripting of AI logic, intended as proof of concept. 
---

# AINodeGraph

During school we had an assignment for an on-going project which was "Pick your own feature". During this I had the idea of implementing an AI runtime scripting feature. In it's current state it's more of a proof of concept than anything but it is fully functional.

My AIBrain / Task Machine works by having a manager which is the "AIBrain" which your AI would inherit from. This class keeps track of, initialized and cleans up any AITask.

The AITask is a base class setup with an overridable function, you would inherit from AITask in your custom Task class and override the OnExecuteTask() function. This function has to return True or False, this is for implementation. It can mean various different things depending on what your task is.
An example is my LookForPlayer task, if the AI can see the player it returns true, if not then it returns false. Every task will execute it-self every tick/frame so it needs to run tick-logic.

The reason for this structure is so that code can be set-up in a similar manner to how you would use something like ImGui.

The NodeGraph works by having NodeGraphObjects (inspired by the K2 nodes in Unreal Engine) which has a lot of virtual functions, this is where you implement all of your nodes functionality and the NodeGraph just calls back to these functions.

The NodeGraphObject is set-up like a linked list that can expand infinitely in every direction (using std::vector) where this list is then used for executing logic during runtime.

Here is an example of the Node Graph:

[Gif](https://cdn.discordapp.com/attachments/875515865540472842/1040638946331349053/Animation.gif)
  
Repository: [AINodeGraph](https://github.com/PrestigeBR/AINodeGraph)
  
## How to use
  
Simple AI Task/State Machine and NodeGraph editor for runtime implementation. Slightly dependant on our schools proprietary engine, "Tengine". Fully dependant on ImGui and ImNodes.

Any use of these codes outside of Tengine will require slight source modifications of varibale types.

![image](https://cdn.discordapp.com/attachments/875515865540472842/1038064190889394196/image.png)

## How to use AIBrain

Inherit your AI from AIBrain, example:


```cpp
class CEnemy : public AIBrain
```

Create Tasks for your AI, these will execute logic on tick and return either true or false so it can be setup in a similar fashion to ImGui.

Initialize your tasks in your AIBrain child class like this:

```cpp
Header:
MyChildAITask* ChildAITask;

Cpp constructor:
InitTask(ChildAITask = new MyChildAITask(this, "MyTaskName"));
```

Then you can either just use these in your update function, if you want to use the NodeGraph then skip this step.

This can look something like this:

```cpp
In Update/Tick Function:
if(ExecuteTask(FindPlayerTask))
    ExecuteTask(PathToPlayerTask);
else
    ExecuteTask(PatrolRandomlyTask);
```

## How to use AI Node Graph

Add ImNodes start/destroy context functions to the same place where you have ImGui start/destroy context functions.

Initialize a new AINodeGraph instance somewhere, and run ```cpp DrawAIGraph();``` in a Tick/Update function.

Now you'll see the NodeGraph.

If you want to create new nodes, look at AINodeObject class. It has virtual functions that you have to override to give it functionality. Check "AINode_Task", "AINode_Sequence" or "AINode_Start" for reference.

The last step is to modify AINodeGraph.cpp' "NODE SPAWN BUTTONS" section to make an ImGui button to spawn your node.

Repository: [AINodeGraph](https://github.com/PrestigeBR/AINodeGraph)
