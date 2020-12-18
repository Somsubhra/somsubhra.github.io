---
layout: post
title: The last 3 weeks in Krita Animation
---

Hello planet! Over the past few weeks I have been working on Krita Animation to make it more usable by adding essential animation features and fixing various loose ends. So here is an update on what has been done so far(Also this happens to be my first update on my Google Summer of Code, 2014 project).

**Fixed loading of animation layers**: Initially the animation layers did not load correctly. Only the first animation layer used to be loaded properly. And there were bugs with the layer box in the timeline GUI too. This has been fixed now. [Here](https://www.youtube.com/watch?v=3VKcvJT8rQ8) is a video demonstrating multiple animation layers and frame switching.

[![Support for Multiple Animation Layers in Krita](https://img.youtube.com/vi/3VKcvJT8rQ8/0.jpg)](https://www.youtube.com/watch?v=3VKcvJT8rQ8)

**Auto frame breaking**: This feature is specifically helpful for animators who don’t like to click the buttons or use the keyboard for adding frames, but directly start drawing on a new frame after selecting the frame. There is an option to disable this feature as it might sometimes get in the way of the workflow. Also there is an option to either insert a blank frame or key frame on frame break. [Here](https://www.youtube.com/watch?v=zHun3tkrjJ8) is a video demonstrating auto frame breaking.

[![Auto Frame Breaking in Krita Animation](https://img.youtube.com/vi/zHun3tkrjJ8/0.jpg)](https://www.youtube.com/watch?v=zHun3tkrjJ8)

**Frame Navigation actions**: Actions for jumping to next and previous keyframes, next and previous frames have also been added with Keyboard shortcuts. This is specifically very helpful for animators who use keyboard to switch frames without clicking the buttons or using the timeline.

![Frame Navigation Actions](https://i.imgur.com/ERZnNTT.png)

**Changing the timeline width**: Added an option to change the timeline width according to the number of frames required in a particular animation.

![Changing the timeline width](https://i.imgur.com/D8OUZCt.png)

**Animation import**: Currently the animation frames and layers get imported in Krita Animation. But the timeline GUI doesn’t get updated accordingly.

**The Road Ahead**

These are the things I have been intending to add or fix in the next few days:

- The Onion skin Docker, which is a critical feature and is currently work in progress. There should be something substantial on this soon.
- Add code to make the timeline GUI refresh/update on its own during import, frame and layer deletion, etc.
- Frame and layer deletion, layer locking, moving frames and layers.
- Animation export to PNG sequences.
- Animation player and scrubbing, caching of probable frames(with some logic like locality of reference).
- …And lots of bug fixes :)

Also there have been some queries about how to test this stuff. So the only way to test it right now is by building from the source code after checking out the animation development branch, which is ‘animator-plugin-somsubhra’.
That is all I have for now. Thanks for reading!

Oh, and by the way Krita started its first donation campaign on Kickstarter to raise money for the 2.9 release and make it more awesome. Here is a direct link to the Kickstarter page: [https://www.kickstarter.com/projects/krita/krita-open-source-digital-painting-accelerate-deve](https://www.kickstarter.com/projects/krita/krita-open-source-digital-painting-accelerate-deve)

![Krita Kickstarter](http://3.bp.blogspot.com/-2FNKM4yhkL8/U5YTz32kjkI/AAAAAAAABvM/vpAUSGmgJz4/s1600/kickstarter_logo2.png)
