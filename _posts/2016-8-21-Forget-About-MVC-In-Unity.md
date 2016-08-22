---
title: Forget about MVC in Unity.
layout: default
---

# Forget about MVC in Unity.

I cannot count the amount of times I have encountered a programmer who seems semi-fond to excited about the subject of MVC in Unity. I have also been asked to describe the merits of MVC in the context of Unity during multiple job interviews. I personally carry the very humble opinion that semi-fond to excited is entirely an inappropriate spectrum of emotions to produce in response to MVC in Unity. The only appropriate emotion is disgust. If one is ever asked to describe the merits of MVC in Unity in a job interview, the appropriate response is, there are none.

MVC is an architecture pattern taught in undergraduate computer science programs. It's very simple, and it's not bad. Separate objects dealing with a database from the objects drawing what the user sees and then separate those from the logic behind them. Reasonable, for the problem domain it was invented for. That problem domain was 2D GUI. Primarily popularized in web applications for implementing backend webpage generation.

2D GUI and backend webpage generation are radically different problem domains than 3D interactive environments. Radically, radically different. Yes you could start to draw parallels. But why take something invented to solve a problem in a radically different paradigm of problems, and contort it to fit something else? Why not just come up with a new architectural perspective conceived of exactly for 3D interactive environments? I think that is the much smarter thing to do. Someone trying to contort MVC to fit an interactive 3D environment demonstrates they have a very limited range of concepts to draw from to conceptualize software architecture in a 3D environment.

To highlight specific issues with it.

Model. This is not a bad concept by itself. If you have a database in your game, it should be contained in an Object. Conceptually a Model object is just fine in a game. But why call it a Model? That is already reserved for 3D Models. How about we instead use the word Data for an object which encapsulates Data. Oh? Because MVC already defined Model for that way back when? Well you know 3D graphics defined the word Model for a Model way before MVC existed. So drop it. An object that encapsulates data is a Data object. Very appropriately named I think.

View. This is one of the worst aspects of it. You really should not have anything named a View in the context of MVC in a game. Because what is your View? Keep in mind in the context of MVC a view class describes how to draw a web page, it has the hard coded positioning, or math to determine placement of elements. The equivalent of that in Unity is your GameObject hierarchy and the transforms, and all of the visual components on them. That is what literally draws your game world. Maybe you could argue that your Camera is your View, this is appropriate. But that is also called a Camera, well named already, and certainly doesn't need a View class describing placement of visual elements to make it work. There is no equivalent of an MVC View in a game world without making an incredibly contrived leap of contortion to do so. It's just bad form.

Controller. The problem with this is that, outside of an object which encapsulates a database, and your GameObject hierarchy which describes how to draw what your camera views, everything is a controller. Everything is implementing the logic to control what you see. The script on your car named, hopefully, Car, is obviously controlling your car. The script on your Player named, hopefully, Player, is obviously controlling your Player. If everything is a controller then the word is just clutter. Of course your script on a GameObject is controlling something. This doesn't mean we need to then have every single script in the project, except for those encapsulating a database, ending with the word Controller or Control. It would be much better if those characters were simply omitted and replaced with other characters more exactly descriptive of what that object actually is, or just have the name be shorter.

I have seen some people reserve the word Controller for more centralized objects which control many things. This is a somewhat more reasonable adaptation of it, versus just appending Controller on almost every one of your scripts. But the times I have seen codebases doing this, the person was actually just using the term Controller to mask what were really God Objects, and poor architecture.

Someone might be thinking, but what if I have a 2D GUI in my Unity game? Well if you are using a web UI framework and you are in the paradigm of web application architecture, for which MVC was invented, that is a great exemption to this criticism. If however you are using Unity UI, much of the same still applies. There is no View class, that is your GameObject hierarchy containing Unity UI components. For your controller, just name it what it is. GameMenu, PauseMenu, NetworkUI etc.

Thank you. I hope to never see the words Model, View or Controller in any Unity project ever again.
