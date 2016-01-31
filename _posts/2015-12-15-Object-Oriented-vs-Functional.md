---
layout: default
---

# Object Oriented vs Functional

A few years ago the phrase arrived to my awareness,
"Object-Oriented Programming is dead in favor of Functional Programming".

Someone had stated this to me based on various other sources of information they had inferred things from, other people repeated it, it continued on. A quick google search "Object-Oriented Programming is Dead" will reveal that this topic has quite a bit of discussion.

People make very rational arguments like, "Paradigms come and go, Object-Oriented is just one". This combined with a lot of hype around "Functional Programming" makes the statement of Object-Oriented Programming (OOP) dying in favor of something else, like Functional Programming (FP), seem plausible.

People who make the priorly quoted statements, or similar to them, are confusing two things. Those two things being, OOP as a philosophical concept of how to design the architecture of software and OOP components implemented in a language.

Java, C++, C#, Objective-C these are languages which have implemented in them components derived from the philosophies of OOP. They are not however the pure and authoritative representations of what OOP actually is. Rather, they are hybrid languages, they are hybrids of some OOP components and Procedural Programming. In the case of C# and Java, there are now components of FP being added to make them OOP, FP, Procedural hybrids.

A language with OOP components, or specific OOP components in a language may die and be replaced with something else. However OOP as a philosophical understanding of how to create the architecture of complex systems will not die. Even if you are in a purely FP language, OOP as a philosophy of architecture still applies and is the ideal perspective to take when figuring out architecture and organization.

OOP in it's most pure and original form, a philosophy of software architecture, is the result of taking the philosophical basis largely developed in the tradition of Hermeneutics and then applying it to the architecture of software and programming language design. To make code comprehensible to people, and allow code to be written in the way the human mind intuitively thinks. This perspective will always be relevant. The history and philosophy of OOP I believe is most thoroughly and properly covered in the book named 'Object Thinking' by David West. If you wish to understand better what OOP actually is, read 'Object Thinking'.

David West in recent years actually made the statement 'Object-Oriented Programming is dead. Long live of Object-Oriented Decomposition and Design'. I think he is recognizing that the term OOP has been fouled, and there is too much convolution and confusion about what it actually is. That people are confusing OOP as an architectural philosophy with OOP as language specific features. Thus rather than fighting to recover the word OOP, and convince most programmers they don't actually know what it is, he is simply making a new term, Object-Oriented Decomposition and Design (OODD). OODD referring to, without confusion, purely Object-Orientation as a philosophy on design of software architecture. This is perhaps a more intelligent stance to take, create a new term. One will use OODD to design the software, but then may implement it in a purely Functional language, or any language. So you end up with an Object-Oriented system implemented in a Functional language.

Personally though, I would prefer people take the time to understand what OOP actually is, and we not just create a new term. We are after all programmers, we think, and rethink things, we don't need PR tricks to reach accurate understanding. This may just confuse people more over time.

OOP is not a programming language, OOP is not a feature of a programming language. Rather some programming languages have some components derived from the philosophy of OOP mixed into them to be a hybrid with other paradigms. First and foremost OOP is a philosophy on the architecture and organization of software. It is not at odds with FP. FP is much more in the problem domain of method implementation syntax. FP is actually in more direct competition with Procedural Programming. For example, Scala largely retains the Object-Oriented features of Java, what is primarily left behind is implementation of methods procedurally, rather they are implemented more functionally. What you result in is Functional method implementation with Object-Oriented architecture. This is the same route .NET is going with F#. Overarching architecture of a system is still Object-Oriented but you have the option of implementing the methods of those objects functionally via F#.

It would be more accurate to say "Procedural Programming is dead in Favor of Functional Programming". The more FP comes into play, the more Procedural will go out. But the programs will still be Object-Oriented in their architecture.

Thus it follows that OOP, and thoroughly understanding all of it's philosophical and architectural concepts is still extremely important, and will always be. Because once you understand the philosophy of OOP architecture, you understand that it is ultimate. If the mind perceives reality in terms of objects and their relations, then it is natural for us to perceive programs in terms of objects and their relations. It will always be important to know what creates a good object in terms of it's name, it's responsibilities and it's relations. Even if that object will be implemented through functional syntax. Even if that object is in a stateless system. If you can't create good architecture in C#, Java or C++, the functional languages are not going to fix that for you. Because architecturally the same exact philosophical concepts are in use.