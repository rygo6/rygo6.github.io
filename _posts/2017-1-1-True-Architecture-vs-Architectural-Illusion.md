---
title: True Architecture vs Architectural Illusion
layout: default
---

# True Architecture vs Architectural Illusion

I notice the notion of Software Architecture gets used in two general viewpoints. One viewpoint is an attempt to make complexity more manageable. Another viewpoint is an attempt to mask complexity. I am going to describe the qualities of these two viewpoints and argue that the prior is how it should be done, and the latter is actually a detrimental practice to the industry. Unfortunately I see the latter as the greater trend.

I believe good software architecture should serve no other purpose than to make the complexity of a project more manageable and more efficient for the developers which will be working with it. Nothing more. I am in favor of mixing paradigms, languages and anything, as long as it makes it more efficient to manage.

I am going to use MVC as an example of one architectural viewpoint which I think actually carries an intent to mask complexity, rather than try to make it more manageable. I believe there is a certain technical dishonesty that underlays it's formation. I believe this came about because certain people vying for more recognition discovered they can appear to be more knowledgable if they took the very complex subject of software architecture and broke it down into a few very simple categories, and a resulting short acronym. Saying it is MVC, versus what would probably be a long technical explanation, is a lot quicker to understand thus probably appears more correct.

I believe trying to fit a complex software project into three categories in no way actually aids the developers working on the project. But rather it creates the illusion of structure. This illusion of structure takes the place of real structure and becomes a detriment to the project.

The group who coined the term MV* rather than MVC I think represents a group that holds a similar recognition to what I just described. The logic behind MV* removes the notion of Controller because of a recognition that it is too broad of a category. Not every object other than a view and model should be conceptualized as a controller, otherwise it becomes restricting. The attempt to force objects to be conceptualized into a constrained term actually causes the architecture to become more convoluted.

This is the essence of why I argue architecture as an attempt make complexity more manageable is ideal, and architecture to mask complexity and make it more presentable is detrimental. Software is complex, this complexity must be dealt with, thats what being a developer means. Attempts to mask complexity by overarching design patterns that are too simplified results in forced conceptualization, less ideal naming and structuring. This actually makes the code base less efficient to manage, even though it may appear more simple and structured to someone not initiated with the codebase.

I am very suspect of all the short acronym quick buzzwords. MVC, MVVC, MVCVC etc. Fitting conceptualization into constrained categories is probably being done for political reasons that don't really aid the those technically involved in the project. when really any object should be conceptualized to be exactly what it is.
