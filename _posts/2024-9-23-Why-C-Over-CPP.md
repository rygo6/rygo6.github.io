---
title: Why C over C++?
layout: default
comments: true
published: false
---

# Why C over C++?

Recently I went through an exercise of writing out a vulkan application in plain C. Trying out a few different C styles in the process. Then I rewrote the whole thing in C++. Trying a few differnent C++ styles in the process. At that point I had probably spent all my spare time over the course of 8 months going through this exercise. At which point I decided to rewrite it all in C again, and stay with plain C.

Why?

## Choice of library affects choice of language.

I would first like to clarify that I believe your choice of language should be heavily influenced by what libraries and APIs you need to accomplish your task. If you need to do some data crunching and there is a great library for your exact problem in python, then python makes perfect sense. If you need to write a REST backend with some database interop then .NET can be great choices because it has good libraries for that.

However when it comes to graphics programming, particularly Vulkan, or OpenGL, the API is itself in C. The Win32 API is also in C. So your starting point is inherently C. In this case it's not a question of "Should I use C?" because you are either way, it's a quesiton of, do you really need anything beyond C?

Generally my conclusion was 'No'.

## C-Like C++ vs C.

There is a whole other subject to be written about the issues Object-Orientation, particularly when it comes to Vulkan and low level programming. So most any C++ feature related to that I just omit, and am comparing C to a C-like C++.

In comparisong to C, when I thought about it, the only thing I'd really miss from C-like C++ were:

1. Default struct values.
2. Namespaces.
3. Occasionally destructors.

In a handful of places I felt these made my code better, but upon further contemplation I realize the benefit these bring don't really outweight the other negatives in C++.

Default struct values can save you repeating many of the sames line of code, namely in Vulkan where everything is defined by info structs passed to a method. But at the end of the day it occured to me, for the purpose of readability of code, it is better to have all the values explicitly listed out in a struct where it is being used because you tend to not remember what the default values are. Having no default values in structs can save lines of code, but at the expense of always have to hunt down what the default values are if something goes wrong.

Namespaces are nice no doubt, but putting a three letter acronym on header methods is also not a big deal. Then you gain the benefit of not having your names mangled, which can be convienent for a handful of reasons. Then you also gain the ability to write single-file header style libraries, or generate single-file amalgrams of a library, in a manner where the compiler has the greatest opportunity to optimize the locality of code blocks. You exchange a purely aesthetic feature for something which can produce better assembly output.

Destructors can be useful, and if you really need them in C, you can use a cleanup attribute in GCC or Clang. However, I found the typical goto cleanup label on error was entirely sufficient for the few times I did need this. Once you type this out it has the nice quality of being explicitly defined in a single method with no hidden control flow.

But what do you gain with C?

## C++ is not a superset of C.

This is a point that I think is often lost today. It is presumed C++ does everything C does, plus more, so why not use C++? But this simply isn't true. Not all C code is valid C++ code and the parts of C that differ are uniquely valuable to low level and graphics programming.

The features which C gives you over C++ are:
1. Compound Literals.
2. Designated Intiializers.
3. Variable Length Arrays on the stack.

These features are particularly significant for graphics programming, particularly Vulkan. As the combination of Compount Literals and Designated Initializers let's you create portable Vulkan code where complex hiearchies of info structs can be nested within each other. Giving you an almost JSON-like style in declaration of all your Vulkan state, yet it compiles down to minimal assembly, even when the compiler isn't set to fully optimized. 

C++20 can kind of get you this if you start mixing std::initializer_list with some clever templates, but it turns into more complexity, and even with -O3 optimizaiton it doesn't always produce comparably minimal assembly. Then unfortuantely C++ put an arbitrary constraint on Designated Initalizers that all values in them must be explicitly ordered the same as they are in the struct. This could be nice for organization, but it unfortunately inhibits you from being able to make macros with a grouping of fields in them that you could add to a Designated Intiializer. Which is a pattern I have found useful in Vulkan, since you do frequently repeat the same grouping of fields in info structs.

Vulkan has many scenarios where you need to request a `count` for an array size, then create an array that size, then send that array back over the Vulkan API to populated. C can do this nicely all on the stack with minimal syntax because it supports Variable Length Arrays. Of course, foregoing MSVC support, but I personally avoid MSVC. Due to the commonality of this pattern in Vulkan, having to resort to the heap to do this because C++ made overly zealous safety decisions just bothers me. 

Those three features that C enables over C++ can realistically allow for simpler and cleaner graphics code. 

But that is only part of it.

##  C++ libaries tend to be bad and huge time sink. 
   
In C you can generally trust a libc implementation to be Okay in highly performance critical scenarios. That it isn't going to go off an do some whacky things behind the scenes or fire off some crazy chain of templates. This makes it easier, and require less mental overhead, and studying of the language and the standard library, to write highly performant code with minimal compile times and optimal assembly.

If you write Vulkan in C++ you end up having to study C++ as much as you study Vulkan. What does that really get you? Objectively speaking, not much. It is mainly all stylistic. 

Perhaps the one more objective benefit of writing such code in C++ or even Rust is that it can give you more safety, but I feel this is a moot point when doing Vulkan or other low level graphics programming. Because you are inherently in one of the most unsafe problem domains irrelevant of the language you are using. Using C++ or Rust for Vulkan programming kind of feels like putting the training wheels on a harley davidson. Yes technically, it may be more safe in some scenarios, but you are kind of missing the forest for the trees.
  
When it came to debugging issues in my Vulkan application, the fact my C implementation still compiles and starts debugging nearly instaneuously has been far more valuable a tool then any static safety analysis of the language. Simply because such static safety analysis wouldn't even catch the Vulkan issues I had. This is one of the problem domains where compile time and debug performance is critical.

##  C++ culture has become a bit whacky.
  
7. A culture around the language with less bikeshedding than other languages., that has many libaries focused purely on the bare essentials of what exactly you need.  won't hound you over superfluous stylistic aspects of code and the latest hip trends like "safety'.
