---
title: ER Objects
layout: default
---

#ER Objects

When I first read this article:
["Don't Create Objects That End With -ER"](http://www.yegor256.com/2015/03/09/objects-end-with-er.html)

I thought it was a bit OCD and unnecessarily nitpicky. It basically says that any class name ending in 'er' is plain and simply wrong. But it intrigued me. So I made a point that throughout the entire codebase of partak I would not use a single object name ending in 'er'.

Now that I have done that, and have a codebase with nothing ending in 'er', I would have to say this is very valuable to do. If you want to improve your skill in architecture and intuition in naming I think you should try to force yourself to do an entire project not ending any object names in 'er'.

I would say about 20% of the time not using er resulted in merely a semantics change, nothing very relevant. But in most cases it caused me to rethink my architecture resulting in better architecture and easier to guess functionality.

Here are a handful of 'er' alternatives that I used:

- Timer -> Clock
- Mover -> Engine
- Listener -> Target
- Manager/Controller -> Display
- Manager/Controller -> Store
- Manager/Controller -> Relay
- Manager/Controller -> Hierarchy
- Manager/Controller -> System
- Manager/Controller -> Config

'Clock' and 'Engine', rather than 'Timer' and 'Mover' I think fall into the generally irrelevant category. These name changes made no significant changes to architecture or comprehensibility.

Changing 'Listener' to 'Target' introduced I think a better description of the object. The term 'Listener' is used a lot in codebases to refer to an object that is awaiting a callback. But it isn't really listening, as in actively doing something. It is better described as a 'Target', as it is another active process which will eventually reach that 'Target'.

Then we get to 'Manager' and 'Controller', this is where it starts to get a bit more obvious. Because I realized my 'Manager' and 'Controller' classes were doing a lot. As you can see from the names. They ended changing into a lot of different things, and a lot more objects.

I realize in retrospect that most people generally use Managers or Controllers to break object-orientation. Meaning, they use them to be a container of many procedural processes that tend to have quirky, or non-obvious interrelation. That when you remove the ability to use the term 'Manager' or 'Controller', or anything ending in er, you end having to think up actually descriptive, singularly specific terms to apply to the description of objects. Which forces you to be more aware of the purpose of each object, and thus more aware of how they relate. Resulting in better architecture.

One of my Controllers was storing references to other objects, running them through a system, and then displaying something. This got refactored into separate 'Store', 'System' and 'Display' objects. It did result in a codebase that I think would be easier for someone else to get a grasp on quickly.

I now interpret encountering the terms 'Manager' or 'Controller' in a codebase to generally signify the point at which the developer most likely got lazy.

Unity uses the term 'Manager' for it's objects which hold configuration settings. 'InputManager', 'QualityManager', 'PhysicsManager' etc. In this case the Managers are really being used as a store for settings. They probably would be better off named 'InputConfig', 'QualityConfig' and 'PhysicsConfig'.

I really cannot think of instance thus far where there is not a better alternative, or at least equally as good an alternative to a name ending in 'er'. I would be very curious to hear about a case where an 'er' name was most certainly the best choice and what your reasoning was. Because so far it seems to be very good advice to not name any object ending in 'er'.
