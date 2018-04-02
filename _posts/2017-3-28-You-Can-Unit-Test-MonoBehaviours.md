---
title: You Can Unit Test MonoBehaviours
layout: default
comments: true
---

# You Can Unit Test MonoBehaviours

Some time ago on the Unity blogs there was a post claiming that you cannot test Monobehaviours. [You can view it here](https://blogs.unity3d.com/2014/06/03/unit-testing-part-2-unit-testing-monobehaviours/).

It recommends separating logic from MonoBehaviours claiming that you cannot unit test MonoBehaviours because 'Every time you try to instantiate a MonoBehaviour derivative you will get a warning saying that it’s not allowed.' The post is referring to the use of the 'new' keyword to instantiate a MonoBehaviour. Which should be expected, as you are only supposed to add MonoBehaviours to GameObjects via the AddComponent method.

So if you desire to unit test a MonoBehaviour why not instantiate it by creating a new GameObject and then using AddComponent on that GameObject?

I have been using this technique for a while now in unit tests and it seems to work just fine without any issues whatsoever. You create a new GameObject, then AddComponent the MonoBehaviour onto that GameObject, run whatever tests you want on that added MonoBehaviour. When the test is done it automatically cleans up the GameObject and Component.

Inside the Unity editor, if you go to Create > Testing > Editor Test C# Script this will produce a new unit test template script with the following code in it.

{% gist rygo6/45768c4c8a8292a8af1e6192e578ae1f %}

As you can see the default template for an unit test which Unity itself ships with is creating a new GameObject in the test. Also given that the unit test automatically cleans up any GameObject created during the test, I believe it is entirely appropriate to create GameObjects during a unit test to test MonoBehaviours.

At this point you may be wondering, what about the Awake, Start and Update methods? You could make them public and call them that way. However, I think Unity has already done abnormal things in this department by making the Unity C++ layer call the private Awake, Start and Update methods. So I consider the MonoBehaviour an unique beast onto which unique solutions are appropriate. It also makes sense from an encapsulation perspective to keep these methods private.

My solution was to write an Utility class to call Awake, Start and Update through reflection so that they could remain private. The code to do this is very short and simple. Of course that is not something you would want to do for any other class. But again, I make an exception for the MonoBehaviour because it is already an abnormality by Unity's own doing.

You want to make sure you call these methods in the proper order of Awake, Start and Update. You can see the full order of events [here](https://docs.unity3d.com/Manual/ExecutionOrder.html). You also want to make sure you don't call anything more than necessary for the unit test. If your unit test only requires Awake to be called, only call that. If it requires none to be called, then don't call any.

This isn't to say don't separate your logic out into other classes and compose them in your MonoBehaviour. Certainly that is entirely appropriate and ideal in many cases, separate your logic out to as many classes as is good for design. Just that, if your only reason to do so is to unit test that class, and you are essentially creating a dummy MonoBehaviour to hold the class, don't. Test the MonoBehaviour directly.

###### *Update March - 30 - 2018*

I have discovered that the team at Microsoft doing the Unity SDK for Windows MR has devised the same solution as myself when unit testing MonoBehaviours. That being, in an unit test you create a new GameObject, add components, then call Awake, Start, Update through reflection. Take a look at their github repo [here](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/master/Assets/HoloToolkit-UnitTests) to learn more.
