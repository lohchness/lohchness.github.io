---
title: Music Visualizer v1
date: 2023-08-10 14:21:00 +0800
categories: [Projects]
tags: [processing, music, art]     # TAG names should always be lowercase
image:
    path: /assets/images/spaceplusone.gif
---

## Music Visualizer

[Code is on GitHub](https://github.com/lohchness/music-visualizer)

Lately I was having a trip down memory lane into my teenage years, and especially the edgy parts of my teenage years. And on the forefront of this memory lane was Monstercat. I was a big dubstep nerd - well, more of an outcast - but Monstercat was the biggest thing to 13-year old me. And I wanted to give coding the music visualizer up a try.

Of course, I had already done a few, but usually with After Effects. I wanted to give it a go with [Processing](https://openprocessing.org/), since: 

- it's a coding language used for visual arts; 

- I've had experience studying and coding up random stuff in it; 

- it has a sound library; and 

- it's forked off Java

I was also inspired by [Raven Kwok's](https://ravenkwok.com/) work on various Karma Fields music videos, especially [Edge of the World](https://www.youtube.com/watch?v=E66v5GOPgkU) which was also done with Processing. I thought that once I get this out of the way, I could be confident enough in my skills to take on a project which I had imagined to be featuring dynamic subdivided cubic cells, which could multiply based on a designated distribution pattern for another music video.

So! The plan was to grab the amplitude of the frequencies from 40Hz to maybe like 2000Hz, map them into an array for the visualizer, process the values for each frame, and draw the values on to the screen. Oh, also spawn dots in the background, and change their velocities according to the volume and beat detector. Sounds easy, right?

Well. For the dots at least.

Turns out how sound is digitally encoded is a lot more complicated than I imagined. More on that later.

## Dots and Spray

The Dots class is pretty simple. It holds a position, and a vector. It also has two diameter variables, one called `base_diameter` and one called `curr_diameter`. This is for scaling its diameter up and down during a beat.

The constructor spawns a dot with a random size and position just outside the left of the screen. The velocity is dependent on its size - the bigger it is, the slower it will travel. If the dot's going too wide, then the vector is multiplied to aim more horizontally.

```java
class Dot {
    PVector position = new PVector();
    PVector vector = new PVector();
    float base_diameter, curr_diameter;
    
    Dot() {
        position.x = START_X_SPAWN;
        position.y = random(START_HEIGHT_SPAWN, END_HEIGHT_SPAWN);
        
        base_diameter = random(MAX_DIAMETER + 1);
        curr_diameter = base_diameter;
        
        vector.x = max( MAX_VELOCITY - map(base_diameter, 0, MAX_DIAMETER + 1, 0, MAX_VELOCITY) , MIN_VELOCITY);
        vector.y = random(-Y_VECTOR, Y_VECTOR);
        while (vector.y > vector.x) {
            vector.y /= 1.5;
            vector.x *= 1.5;
        }
    }
}
```

The Spray class contains all Dots, and manages each of them. The `sprayDots` function spawns a new Dot every five frames, and updates their position by their vector, and size and velocity by the current track's volume or beat. The dot's size is multiplied by a constant on a beat, and decreases down to its `base_diameter` over time.

```java
void sprayDots() {
    if (frameCount % 5 == 0) {
        spray.addDot(new Dot()); 
    }
    float curr_level = track.mix.level();
    
    fill(255);
    for (Dot dot : spray.dots) {
        ellipse(dot.position.x, dot.position.y, dot.curr_diameter, dot.curr_diameter);     

        dot.position.x += dot.vector.x * 8/3 * exp(4 * curr_level - 2);
        dot.position.y += dot.vector.y * 8/3 * exp(4 * curr_level - 2);

        if (dot.curr_diameter > dot.base_diameter) dot.curr_diameter -= 0.05;
        if (beat.isOnset()) dot.curr_diameter = dot.base_diameter * 1.25;           
    }
    
    
    //clean up
    for (int i = 0; i < spray.dots.size(); i++) {
        Dot dot = spray.dots.get(i);
        if (dot.position.x > WIDTH + dot.curr_diameter || dot.position.y > HEIGHT + dot.curr_diameter) {
            spray.removeDot(dot);
        }
    }
    
}
```



## The Visualizer

## The Rest

But I had a working version. I'm missing about half the spectrum - the bass - if you compare it to a Monstercat video, but it works well enough. Most of the work left is to just pore through the sound library Minim's documentation to look for the correct functions to use to get the lower half of the spectrum. Then maybe refactoring some of the code for processing the values before being drawn. But! Here is the (half) working version in high quality and 60 fps:

<iframe width="560" height="315" src="https://www.youtube.com/embed/5qB2VDdLEVU?si=4P5UYPzMDToznWX-" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

The source code is available on [GitHub](https://github.com/lohchness/music-visualizer).

So how is audio encoded digitally?

## How sound is encoded digitally

Who fuckin knows. # TODO: Expand here