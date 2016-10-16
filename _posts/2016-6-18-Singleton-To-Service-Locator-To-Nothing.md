---
title: Singleton to Service Locator to Dependency Injection to Nothing
layout: default
---

# Singleton to Service Locator to Dependency Injection to Nothing.

I find that people use the singleton pattern in unity heavily. I did this as well in the beginning. Singletons are simple, easy to access and easy to create. I do however think they promote bad architecture as your project grows, and you also run into problematic areas with them. This only became apparent to me once I began to work on projects with considerably large codebases.

I was working on one project that was fast approaching over 40 Singleton Manager classes. The project had in it defined the notion of a Singleton Manager as a central access point, and everyone else followed this notion. The problem with this however, and those 40+ Singleton Managers, is that the roles of those objects were really not the best suited to being a Singleton, nor a Manager.

A handful of those classes would of actually been better used if we could have a multiple instances of them. But the classes worked around this internally by complicating their code so they could adhere to the Singleton Manager precedent. Another handful of the Singleton Managers would have been useful if we could inherit from them and have a few variations on their base functionality. But this was avoided to retain the already in place Singleton Manager precedent and the code made more complex to work around it. Another handful of them really just were not Singleton Managers conceptually, but were made to adhere to it out of precedent.

Ultimately the precedent of having Singleton Managers be a common pattern in code for central scripts was making the codebase more contrived than it was helping it. When you really analyze what a Singleton is for, it's simply to get access to an instance of object. There are other ways of doing it. So why not set precedent of how to do this in a way that will not lead to contrived code once your project grows?

Thus I have come to the opinion of, do not use the Singleton pattern.

After that I began to work on a codebase that had a very comprehensive and thorough implementation of the Service Locator Pattern. This was seemingly an upgrade over a mass of Singleton Managers. As it allowed you to have multiples and also inherit from classes in it. However one negative to the Service Locator I had found was in the defining of things as a Service. Not everything that needs to go into the Service Locator is actually a Service conceptually. But none the less due to the precedent of the Service Locator, things were made to conceptually contort to fit the notion of being a Service. The code was less contrived than a mass of Singleton Managers, but I think conceptually is was still somewhat contrived.

Next I happened upon someone who was adamant about Dependency Injection as an ideal replacement for anything like a Singleton or Service Locator. I liked Dependency Injection conceptually. It was very open ended, and required no contriving of code in implementation nor conceptually to fit any pattern. It's syntax for connecting things is simple.

I steered away from Dependency Injection however when starting a new project because you must import a Dependency Injection framework, which are not small, nor simple. Something seems strange to me about having to import a codebase, larger and more complex than my actual codebase, to do the very simple task of hooking together objects.

Perhaps as the code in my new project grows, Dependency Injection may seem more appropriate. But it also seems to me that Dependency Injection is really breaking Object Orientation philosophically for the purpose of syntactical sugar. If you design your objects correctly, and the architecture of code correctly, I really have to question. Will the relations between them become so difficult to manage that you need Dependency Injection? My current impression of Dependency Injection is that it's something that someone needs when their objects and their relations are a bit contrived and becoming difficult to manage. That really Dependency Injection isn't something to aspire to, but is a patch put on something becoming difficult.

Which brought me full circle back to simply, Find, FindWithTag and FindObjectOfType already built into Unity. I really do believe that for most Unity projects these three things are entirely sufficient and all that you need. The Find methods are in essence the built in equivalent of the Service Locator Pattern in Unity. Due to them being built-in, and their simplicity, utilization of only those methods to connect instances will result in a much simpler codebase.

There is a drawback to Find, FindWithTag and FindObjectOfType, that being, they have a seek time and their seek time increases with the amount of objects in a scene. This can generally be evaded by setting up all references in the Awake method. For most projects this won't be an issue, most Unity projects are generally simple with not many objects in them. Thus the seek time of the Find methods will be barely measurable. Even if you have to Find something while the game is running, for most Unity projects this won't even be noticeable. So seeking to optimize this preemptively without a specific reason is not really justifiable.

If you are however planning to create a game which will have 10,000+ objects in a scene, like an open world RPG, or other. It may be justifiable to think about this before-hand. In this case I think one solution could be something along the lines of a Service Locator implementation, but conceptually it does not require things to be bound to being a Service.

But really, I think, if you design the architecture of a project correctly. You can entirely evade the need to fetch references of objects anywhere in the entire world in a fashion so open-ended, while the game is running, that it requires a Service Locator type implementation.

For example, one of the most common needs of FindObjectOfType while the game is running is after you Instantiate a new object, you need to hook up it's references. Using Find methods in this case can be evaded by Instantiating new objects through a Factory of some kind. The Factory implementation would gather the appropriate references on Awake, then fill them in onto what it Instantiates.

Objects needing to reference other objects by proximity are most ideally retrieved through Raycast and ColliderInfo metadata.

I do believe that if you have a well designed hierarchy of objects, their responsibilities, and their relations. The need to use anything like Dependency Injection, Singletons or a Service Locator can actually be entirely evaded without any negatives, resulting in much less contrived code, and better architecture. As it forces the relations in your design to be much more explicitly defined and structured, rather than able to freely connect any which way. Maybe I will find this to be incorrect at some point, but for now I will continue on with only Find methods in Awake and well thought out architecture.
