---
title: Unity Object Component Orientation
layout: default
---

# Unity Object Component Orientation

Typically each separate class in C# denotes itself as being a separate Object. Thus for each class, one should expect the class to be following the principles of being an Object. However in Unity I would contend that there are actually two different domains which a class can represent. Those are an Object, and a Component.

Unity works by adding Components to GameObject's. In an Unity scene one GameObject can be described by multiple Components, or rather, multiple classes. In a purist Object Oriented sense, a class name should be a noun which does verbs because a class is an Object, and an Object is a noun. In a purist Object oriented sense a class should not be a verb, nor an adjective, because those are not nouns, they are not Objects, they are not actually existing items. But in the context of Unity the actually existing item, the Object, is the GameObject. Does it then make sense that every Component added to that GameObject is too itself an Object with a noun name? Some Components may actually only modify the GameObject, some Components may cause the GameObject to do an action. If this is the case, which it is, shouldn't we name those Components accordingly? As adjectives and verbs?

I think we should. If I am creating a Component which rotates a GameObject. Rotate is a sufficient name for the class. To try and come up with a noun name, like Axis or Wheel, actually convolutes and confuses the Components purpose. It's purpose being something purely abstract, which causes an action to occur on a GameObject, it rotates. Thus Rotate is the most simple and descriptive term to name the Component. A Rotate Component may then be paired with a Wheel Object.

It's on this thinking that I propose Unity needs to be considered a somewhat unique paradigm from purist Object-Orientation. Unity is Object-Component-Orientation. Objects, which of course are still needed, should be named nouns. But if you are a creating a Component which is a modifier or something which causes an action upon a GameObject, name it what it is, an adjective or a verb. The Object-Orientation in this is still, somewhat abstractly, retained because the architecture and layout of mechanics would be orientated around the GameObjects.
