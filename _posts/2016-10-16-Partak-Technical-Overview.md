---
title: Partak Technical Overview
layout: default
comments: true
---

# Partak Technical Overview

My personal game named 'partak', condensed from 'particle attack', is one my favorite projects. It is a remake of an old game that came from the open source community in the mid 90's called 'Liquid Wars'. The game 'Liquid Wars' I thought was a brilliant gameplay mechanic, on par with any of the classic games such as Tetris, or Pac-Man. But for some reason it never achieved comparable notoriety. To date, I believe partak is still the only 'Liquid Wars' clone anyone has made. I suspect part of the reason for this is because it's gameplay mechanic is quite a bit more difficult to implement than other classics.

Me being a fan of 'Liquid Wars' and also being a fan of difficult algorithms, and wanting to see this game live on in the mobile world is what inspired me to create 'partak'.

The algorithm underlying 'partak' is a quad-tree optimized implementation of the Dijkstra's algorithm. This is a very old, and simple, path finding algorithm. However despite it being so old, it still offers some unique advantages over modern path finding system. The primary benefit being that it can path find 5000+ particles at a sustained frame rate to a single point on iPad 2 level hardware.

 The essence of this algorithm is you first create a grid of cells over the area which you want to path find. You then choose a starting point within that grid and step out in each direction from that cell. Each new cell you reach in that step you store what direction it was stepped to from, then repeat the same process for each one of those new cells. You let this run recursively, stepping out and spreading throughout the entire grid, until it can find no more. You have then just calculated the direction which each cell needs to pass it's contents off to in order to reach the single target point in the grid.

 Running this process through a quad tree rather than a flat grid greatly accelerates the process by many many folds. The logic is essentially the same. You step through each quad tree node at the highest level of the tree that you can. Once a direction is calculated for that node you give all of it's children the same direction.

 Here you can see this running in this video. The longer red lines represent that it is farther from the target point.

{% include youtubePlayer.html id="32UH7VGHRPY" %}

Once you have this quad-tree of directions calculated, then moving something through it is as simple as looking at which grid cell your content is in, what direction that cell has recorded, then moving your content that direction. Repeat at whatever rate you desire for whatever speed you desire.

Here you can see some particles moving through the grid. The random jitters in the direction lines at the end of this video is intentional, I found it made the resulting movement appear more organic.

{% include youtubePlayer.html id="ocor8j1PXkk" %}

Moving content through the quad-tree is extremely cheap, literally just a single look up of an int. This is why it can move 5000+ particles on an iPad 2 at a sustained frame rate. The processor intensive part is the calculation of all of the directions in the quad-tree. But once that is calculated many many particles can use that data to path find simultaneously.

In 'partak' the calculation of the directions in the quad-tree are done asynchronously in a separate thread. This calculation must be separated out from the main thread on lower end mobile hardware for sustained frame rate, as it will consume nearly an entire CPU.

The path-finding algorithm is set up in a way where it does it's calculation entirely self-contained and then populates a large array of ints representing the directions. The main thread looks at the appropriate direction it needs in this array and then steps it's given particle that direction. Due to everything interfacing through a simple array of ints, which are atomic, this system does not actually need any locks. Which is ideal, because in performance critical algorithms like this, placing a lock incurs a significant performance hit. Since the results are so chaotic, if the main thread takes half the directions from the current cycle, and half the directions from the prior cycle of quad-tree direction calculation, you actually cannot tell.

Below you can see a gist of a basic outline of a class that would operate like this.

{% gist rygo6/72208c2200880c222c7169532d4d4bcf %}

I would like to note that gist is extremely simple. If you intend to seriously use a setup like this I have created a library called [ECThreading](https://github.com/rygo6/ECThreading) which is a collection of my learnings on how to do this type of multi-threading in Unity properly.

'partak' is available for free on both the [iOS App Store](https://itunes.apple.com/us/app/partak/id639879646?mt=8) and the [Android App Store](https://play.google.com/store/apps/details?id=com.technologicalmages.enrgy&hl=en). Where it has long held about a 4+ star average rating with many rave reviews.
