---
layout: post
title: First steps towards Animation in Krita
---

For the last few weeks, I have been working on adding animation support in Krita, which has also been accepted as my Google Summer of Code project.

To get things moving, I have added a new timeline interface for creating and editing animation frame-by-frame. The timeline has a separate layer box, which has been adopted from Krita’s existing Node Model(The layer box still has vital features left out though).

The other vital part is the Animation Frame Box. A look into the internals of the Animation Frame Box looks like this: The Frame Box consists of a list of Layer Contents(a collection of frames in each layer). Further each layer content consists of a list of Animation frames. Each animation frame can be of two types: blank/empty frame and xframes. A blank frame would contain no data on the canvas while an xframe would contain data on canvas. Every animation frame could be of varying length and the length would also necessarily depend on the neighboring frames.

Now a bit about frame insertion dynamics: A new instance of animation would start with a layer with a blank frame. If the canvas gets modified the blank frame turns to an xframe.

![The timeline on starting a new instance of animation](http://1.bp.blogspot.com/-B_w_8WrkX50/UcdDqUH2zRI/AAAAAAAAAGU/P4amp-ZyctM/s1600/11.png)

As of now there are three frame insertion actions.

Next adding a blank frame would insert a blank frame at the current selection plus extend the width of the previous frame to its beginning.The width of the new frame would depend on the next frame(if there is one).

![Adding a new blank frame at a selection](http://2.bp.blogspot.com/-r_FydrqLMsY/UcdEI51nQeI/AAAAAAAAAGc/eIhYbDsp-tg/s1600/22.png)

Adding a frame would extend the frame to the corresponding selection.

![Adding a frame extends the previous frame from the selection](http://3.bp.blogspot.com/-xd9fyaZ4fSk/UcdEVTSVhZI/AAAAAAAAAGk/lfU7olOFhP0/s1600/44.png)

Adding a blank frame in between a current frame

![Adding a blank frame in between a current frame](http://1.bp.blogspot.com/-f7V5Vy48So0/UcdEeQCwBGI/AAAAAAAAAGs/Lqyq-Y6Ajhc/s1600/55.png)

Adding a new layer would insert a blank frame with same content length as that of the previous layer.

![Adding a new layer adds blank frames to it](http://2.bp.blogspot.com/-t87PxQB_MSQ/UcdE3QIG2VI/AAAAAAAAAG0/0D4a07z2YMA/s1600/66.png)

So what next? I am now working on developing a frame switcher which would switch the canvas views. Each frame would contain a reference to the corresponding .kra file. And then I can start on the more challenging stuff: creating an efficient file format for storing the animation. More details on the proposed file structure can be found here. 

If you are interested in tracking my progress, the branch name on Calligra is ‘animator-plugin-somsubhra’.

Lastly I would like to thank Boud, Animtim and Sketchstick  without whose inputs and feedback, this would not have been possible. Also thanks to the wonderful KDE community and Google for accepting my project for GSoC 2013.
