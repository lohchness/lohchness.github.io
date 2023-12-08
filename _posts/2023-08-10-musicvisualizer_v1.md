---
title: Music Visualizer v1
date: 2023-08-10 14:21:00 +0800
categories: [Projects]
tags: [processing, music, art]     # TAG names should always be lowercase
image:
    path: /assets/images/spaceplusone.gif
---

## Music Visualizer

[GitHub](https://github.com/lohchness/music-visualizer)

Lately I was having a trip down memory lane into my teenage years, and especially the edgy parts of my teenage years. And on the forefront of this memory lane was Monstercat. I was a big dubstep nerd - well, more of an outcast - but Monstercat was the biggest thing to 13-year old me. And I wanted to give coding the music visualizer up a try.

Of course, I had already done a few, but usually with After Effects. I wanted to give it a go with [Processing](https://openprocessing.org/), since: 

- it's a coding language used for visual arts; 

- I've had experience studying and coding up random stuff in it; 

- it has a sound library; and 

- it's forked off Java

I was also inspired by [Raven Kwok's](https://ravenkwok.com/) work on various Karma Fields music videos, especially [Edge of the World](https://www.youtube.com/watch?v=E66v5GOPgkU) which was also done with Processing. I thought that once I get this out of the way, I could be confident enough in my skills to take on a project featuring dynamic subdivided cubic cells, which could multiply based on a designated distribution pattern for another music video.

So! The plan was to grab the amplitude of the frequencies from 40Hz to maybe like 2000Hz, map them into an array for the bars, process the values for each frame, and draw the values on to the screen. Oh, also spawn dots in the background, and change their velocities according to the volume and beat detector. Sounds easy, right?

Well. For the dots at least.

Turns out how sound is digitally encoded is a lot more difficult than I thought. More on that later.

But I had a working version. I'm missing about half the spectrum if you compare it to a Monstercat video, but it works well enough. Most of the work left is to just pore through the sound library Minim's documentation to look for the correct functions to use to get the lower half of the spectrum. Then maybe refactoring some of the code for processing the values before being drawn. But! Here is the (half) working version in high quality and 60 fps:

<iframe width="500" height="250" src="http://www.youtube.com/embed/5qB2VDdLEVU" frameborder="0"> </iframe>

The source code is available on [GitHub](https://github.com/lohchness/music-visualizer).

So how is audio encoded digitally?

Who fuckin knows. # TODO: Expand here