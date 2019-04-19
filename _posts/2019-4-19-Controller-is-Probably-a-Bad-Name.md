---
title: Controller is Probably a Bad Name
layout: default
comments: true
---

# Controller is Probably a Bad Name

In the world of Model View Controller and web development, you end up with a codebase where every class ends in either Model, View or Controller. I have wrote a [bit](http://rygo6.github.io/2017/03/26/ECS-not-MVC.html) in the [past](http://rygo6.github.io/2016/08/21/Forget-About-MVC-In-Unity.html) about how you really should not think of Unity projects in an MVC context, and I don't think most people at this point in time do. Much of the web development world itself has even moved past the MVC conceptualization with React. React actually has an architectural perspective more similar to Unity, in that it is all about composing more generic components.

 However I still come across Unity projects where every single component ends in Controller. Which is really just unnecessary. [Scroll down the list of all components that ship with Unity.](https://docs.unity3d.com/ScriptReference/Application.html) Imagine if each one had 'Controller' appended to the end, ApplicationController, ClothController, FlareController. That seems pretty silly doesn't? But yet some people think they need to put the name Controller on the end of every component which controls something. I contend using the term Controller to describe a component that controls something is probably bad naming. Controller is such a non-descriptive, generic and borderline irrelevant name. There are so many more descriptive names for a component. Using these more descriptive names I think will both aid you in better separation of concerns in your architecture, and also make your code easier to follow.

To further illustrate I have compiled a list of nouns that could be used to name components.

- Sequence
  - For a component which either coordinates a sequence of something.
- Catalog
  - A component which holds a reference to many other objects, but serves no additional purpose than being a central point to access those other references.
- Factory
  - A component which you go to in order to spawn some of other component.
- Root
  - A component which is the root point of a hierarchy of other components, or the entry point into a system of components.
- Container
    - Any component that represents a root level of a more complex prefab, and requires more components as children of it. Conceptually similar to Root, but I would expect a Container component to in some manner actually contain its children in the game world.
- Renderer
  - Any component which renders anything, either through post-process effects or by procedurally generating meshes.
- API
  - Any component that serves as the interface to some other system, or maintains a connection to some backend system.
- UI
  - Any component which describes the logic for an entire user interface. Usually I have an UI component at the root of a UI canvas which acts as the central point to coordinate things in that specific canvas. All children components in the canvas can then get the UI component they belong to by doing GetComponentInParent or transform.root.GetComponent.
- Menu
  - Any component which describe an interactable UI panel. Usually I place menu components on panels which represent singular menus in a larger canvas based user interface.
- Database
  - Any component that wraps a database.
- Datum
  - Something which does nothing but contain data, most ScriptableObjects I create which do nothing but store data I end up calling a Datum.
- Item, Piece, Part
  - Any component which represents a singular piece among multiples.
- Pool
  - Any component which holds references to many other components to be recycled.
- Group
  - Any component which represents a grouping of simple parts.
- Wrapper
  - Any component which wraps a third party API, or other, to translate its data, or unify its API calls.
- Layer
  - Any component which represents a single layer of something which would generally be stacked on top of each other.
- Behaviour
  - Any component which extends MonoBehaviour and provides a base type of Behaviour in a more specific context.
- Processor
  - Any component which receives data, does some form of processing, and then passes it on in some fashion.
- Interaction
  - Any component which receives inputs from the user and then affects the game world in some way.
- Description
  - An object which holds a description to be loaded into another object, or component, to then construct itself off this description.
- Relay
   - A component which relays something, such as data or an event.
- EventTrigger
  - Unity uses this name itself for components which receive an event from the Unity EventSystem then affects the world in some manner.

The following list of component names is more generic, but may be unavoidable. I would content though if you are doing it correctly only a small percentage of your components should carry one of these names.

- System
  - A component which is the entry point to any more complex system. This is conceptually similar to both Root and Container, but could be used when neither Root nor Container is an applicable concept in your system. You may also want to consider if your System actually needs a centralized System component or could be designed to function without it.
- Service
  - Any component which is to be universally accessed, either in a scene that never unloads or has been marked DoNotDestroyOnLoad. Database, API and Wrapper could all be better names if they better describe your component, but sometimes you may end up with Service components.
- Manager
  - Any component which contains many references to other components and manages them. The term Manager implies there are subordinates, so unless the Manager actually contains a List of references to other components which it manages, then you should probably use System or Service. Sequence, Catalog, Renderer, Pool, Container or Root could all be more descriptive names for your component, but sometimes that is not always so, at which point deferring to just Manager can be appropriate.
- Coordinator
  - The inverse of a Manager. If your component does not contain a List of components it manages, but rather many other components find this component in order to be coordinated, it is probably more a appropriate to call it a Coordinator. However you should consider if you can design the system in manner which doe snot require a central coordinator.

By no means consider this list some kind of absolute reference. If you end up naming a component 'GroupManagerWrapperServiceSystem' then I think you really missed the point.

Rather, I am trying to illustrate how many other options exist to name components, and also objects. This is an inexact art, but I contend it is really one of the most important things to do correctly. You should always strive to name components and objects as specifically and minimally as possible.

These is a quote that has floated around for a while that goes, "There are only two hard things in Computer Science: cache invalidation and naming things." I don't know so much about cache invalidation as the primary one. But naming things is something I would put high up on the list of difficult to get correct things that most do not realize the depth nor importance of. An idealism in Object-Orientation is if you can name all of your objects well enough, you do not need documentation, because each objects name already describes so well it's role in the mechanics of the entire system. In practice I don't think you can ever get away without any documentation, but a system with good names makes a huge difference in the ease of maintaining it and also collaborating with others. Good names also greatly aid you in conceiving of better architecture and better separation of concerns, which is why it is important to put effort towards this from the very beginning. Poorly performing methods in a class can always be refactored, it is easier to correct that at any point. However if you used poor naming, and thus have poor taxonomy through your entire system design, then you probably ended up with poor separation of concerns. Then to correct that probably would require a substantial re-architecture and refactoring of much of the system.
