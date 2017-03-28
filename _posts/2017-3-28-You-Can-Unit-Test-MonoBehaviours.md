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

Given that it automatically cleans up the GameObject and Component at the end of each unit test. It's almost as though Unity designed their specific implementation of NUnit with the intention to let you create GameObjects in the unit test.

Inside the Unity editor, if you go to Create > Testing > Editor Test C# Script this will produce a new unit test template script with the following code in it.

{% gist rygo6/45768c4c8a8292a8af1e6192e578ae1f %}

As you can see the default template for an unit test which Unity itself ships with is creating a new GameObject in the test. Unity really did design their specific implementation of NUnit to deal with newly made GameObjects, and naturally anything added to them, inside an unit test.

I am kind of wondering whats going on here? Why did that Unity blog post insinuate that you can't Unit Test MonoBehaviours? Did the author of it really just not know that your supposed to create a new GameObject and use AddComponent on it? I doubt it because the writer of that post is someone who heavily worked on the Unit test framework in Unity.

I think one of two things potentially occurred.

1. That blog post is old and the Unity unit test framework has since been updated to deal with GameObjects created in Unit tests. This is very likely as that Editor Test C# Script template did not actually appear in Unity until I think version 5.4, which was released long after that blog post.

2. Due to some reasoning of formality stated in a TDD book printed years ago before the problem domain of Unity even existed. It was assumed improper to instantiate an object through any means other than the new keyword. It was also assumed most proper to instantiate as few objects as possible to do a unit test.

I think it is probably reason #1 because reason #2 I do not think is a good reason.

The objective of being a software engineer is not to simply follow process but rather to actively invent new solutions and workflows to problems. The intention of that invention process is to make yourself more efficient, more productive and produce code that is more maintainable.

If you were to follow the Humble Object Pattern you would end up with twice as many classes and unnecessary additional code. That wouldn't make you more efficient, nor more productive and it would make the codebase less maintainable.

The Humble Object Pattern at this point in time is a bad idea.

People who have contrived MVC to be the Humble Object Pattern, such as [this person](http://jacksondunstan.com/articles/3092), I also think that is a bad idea at this point in time. I also think contorting MVC to fit Unity is a further bad idea for [this reason](http://rygo6.github.io/2017/03/26/ECS-not-MVC.html) and [this reason](http://rygo6.github.io/2016/08/21/Forget-About-MVC-In-Unity.html).

At this point you may be wondering, what about the Awake, Start and Update methods? You could make them public and call them that way. However, I think Unity has already done abnormal things in this department by making the Unity C++ layer call the private Awake, Start and Update methods. So I consider the MonoBehaviour an unique beast onto which unique solutions are appropriate. It also makes sense from an encapsulation perspective to keep these methods private.

My solution was to write an Utility class to call Awake, Start and Update through reflection so that they could remain private. The code to do this is very short and simple. Of course that is not something you would want to do for any other class. But again, I make an exception for the MonoBehaviour because it is already an abnormality by Unity's own doing.

You want to make sure you call these methods in the proper order of Awake, Start and Update. You can see the full order of events [here](https://docs.unity3d.com/Manual/ExecutionOrder.html). You also want to make sure you don't call anything more than necessary for the Unit test. If your Unit test only requires Awake to be called, only call that. If it requires none to be called, then don't call any.

So my recommendation is to unit test the MonoBehaviour directly. I have been using this process and it works well without any issues. Then you do not need to double the amount of files in your codebase and write unnecessary code, making you less efficient, less productive and your codebase less maintainable. All of which I consider to be much greater negatives than having to use an unique alternative to unit test the unique beast that is the MonoBehaviour. Plus you actually get better test coverage since you are not omitting the contents of your MonoBehaviours from tests.
