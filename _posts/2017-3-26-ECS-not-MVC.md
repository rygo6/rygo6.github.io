---
title: ECS not MVC
layout: default
comments: true
---

# ECS not MVC

I am going to expand a bit more on my [prior post](http://rygo6.github.io/2016/08/21/Forget-About-MVC-In-Unity.html) about not doing MVC in Unity. As my prior post does not elaborate on the actual architectural difference, so it could be confused as just a semantics difference.

I have had the great opportunity to interview many different Unity developers over the past year. I am always amused with the ones who proudly list MVC as a prominent design pattern on their resume. Simply listing this in relation to Unity is suspect to me, but not entirely irrelevant. After all, understanding the separation of concerns in MVC is valid and important.

Of all people who relate MVC to Unity I have begun to ask them one question, "Do know what design pattern Unity itself uses?". Not one has answered this question correctly. The answer I am looking for is [Entity Component System](https://en.wikipedia.org/wiki/Entity–component–system), or ECS. Technically Unity is not a strict ECS implementation, but a derivative of it. The point of this is that ECS comes with it's own intention of how to design systems which is not in full congruence with MVC.

The essence of ECS is that you have your entity, or GameObject in Unity, which is decorated with Components. The composing of those components describes the behavior of that entity in the game world. The intention of this is you end up with a multitude of different components to compose in different ways for the purpose of creating new behavior on entities without new code.

This viewpoint of system design goes in direct opposition to the notion of strictly following MVC. Now do not misunderstand, it's not in direct opposition to the notion one should separate objects which deal with logic from those which deal with presentation. Separation of presentation and logic is a good separation of concerns. The problem comes in the notion that defined behavior should have a Controller class and corresponding View class, and these two classes should be tightly coupled.

The intention of ECS is to remove the need of a GameObject to have a corresponding specific class to describe it's behavior, but rather have it's behavior produced by the composition of generic components. Now do not misunderstand that either, you will at times end up with a Component which describes behavior for one specific entity, it's unavoidable. However, under ECS it is more ideal to have generic reusable components, none of which are tightly coupled to another. This is why conceptualizing a system into Controllers that have their corresponding Views is bad in ECS. You want completely generic components which can be composed every which way.

For example. If you have the need of a GameObject to fade in and out, or pulse, or sparkle. All presentation related behaviors. This should not go in a View class directly corresponding to the logic class of that entity. Rather those should go into separate components which do only those specific things, Fade, Pulse and Sparkle. You then reuse those components anywhere such a visual effect is necessary. The logic component can then find and use all of those separate presentation components as necessary.

At times you may end up with certain presentation needs which are highly unique to the logic of your entity and thus end up with a presentation class specifically for it. This is appropriate, it just not the ideal intention for the entire system to follow. The ideal is generic composable components.
