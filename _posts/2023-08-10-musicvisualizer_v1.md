---
title: Music Visualizer v1
date: 2023-08-10 14:21:00 +0800
categories: [Projects]
tags: [processing, music, art]     # TAG names should always be lowercase
image:
    path: /assets/images/spaceplusone.gif
---
<link rel="stylesheet" href="{{ site.baseurl }}/assets/css/adds.css">

## Music Visualizer

[Code is on GitHub](https://github.com/lohchness/music-visualizer)

Lately I was having a trip down memory lane into my teenage years, and especially the edgy parts of my teenage years. And on the forefront of this memory lane was Monstercat. I was a big dubstep nerd - well, more of an outcast - but Monstercat was the biggest thing to 13-year old me. And I wanted to give coding the music visualizer up a try.

Of course, I had already done a few, but usually with After Effects. I wanted to give it a go with [Processing](https://openprocessing.org/), since: 

- it's a coding language used for visual arts; 

- I've had experience studying and coding up random stuff in it; 

- it has a sound library; and 

- it's forked off Java

I was also inspired by [Raven Kwok's](https://ravenkwok.com/) work on various Karma Fields music videos, especially [Edge of the World](https://www.youtube.com/watch?v=E66v5GOPgkU) which was also done with Processing. I thought that once I get this out of the way, I could be confident enough in my skills to take on a project which I had imagined to be featuring dynamic subdivided cubic cells, which could multiply based on a designated distribution pattern for another music video. Here's a demo:

![](/assets/images/octtree1.gif)

![](/assets/images/octtree2.gif)

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

Here's me manually pulsing the dots, then unpausing the track to demonstrate the velocity and size increase with the beat.

<iframe width="750" height="700" src="https://www.youtube.com/watch?v=dj_R4YeGpKM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## The Visualizer

The real meat of the code.

```java
fft = new FFT(track.bufferSize(), track.sampleRate());

fft.logAverages( 100 , 20 );
fft.window(FFT.HAMMING);
fft.forward(track.mix);

bar_length = new float[fft.specSize()];
target_length = new float[fft.specSize()];
for (int i=0; i<fft.specSize(); i++) {
    bar_length[i] = 0;
    target_length[i] = 0;
}
```

What `fft.logAverages(100,20)` does is calculate averages based on a minimum octave width of 100Hz, split into 20 bands. The variables `bar_length` and `target_length` are for easing the transformation of the orange lines/bars.

Unfortunately it doesn't seem to work - there is still a steep slope leading up on the leftmost side of the visualizer. So, if you look below, I added a shitty bandaid solution to smooth out this curve. I also modified the values of the latter part of the curve to make it appear more natural.

```java
for (int i = 0; i < BARS - 10; i++) {
    
    if (target_length[i] < BAR_MAX_LENGTH) {
        target_length[i] = BAR_MAX_LENGTH;
    }
    
    // SHITTY SOLUTION TO A PROBLEM
    // if first few number of bars then get average of next bars to smooth out curve
    if (i==0) {
        target_length[0] = (target_length[0] + target_length[3] + target_length[5]) / 4;
    }
    else if (i == 1) {
        target_length[1] = (target_length[1] + target_length[4] + target_length[6]) / 4;
    }
    else if (i == 2) {
        target_length[2] = (target_length[2] + target_length[5] + target_length[7]) / 4;
    }
    
    //increase size and sensitivity of latter part of bars according to sine wave
    if (i > int(BARS * 1/3)) {
        float mult = ((pow(sin(counter),2)) * 5 ) + 1;
        target_length[i] *= mult;
        counter += .15;
    }
    
    if (target_length[i] < BAR_MAX_LENGTH) {
        target_length[i] = BAR_MAX_LENGTH;
    }
    
    // ease rectangle transform
    float targetX = target_length[i];
    float dx = targetX - bar_length[i];
    bar_length[i] += dx * EASING;

    rect(currx, startY, BAR_WIDTH, bar_length[i]);
    currx += 15;
    target_length[i] = 0;
}
```

To smooth the leftmost side even further into a wave, I added some bars further left:

```java
// draw bars before first
// smooth out left side of the visualizer, looks more like a wave than a slope
int preX = startX - BAR_GAP;

for (int i=NUM_BARS; i>0; i--) {
    float mapped = map(bar_length[ NUM_BARS - i ],0,BAR_MAX_LENGTH, 0, 1);
    float bar_height = pow(sin(mapped),2) * BAR_MAX_LENGTH;
    rect(preX, startY, BAR_WIDTH,  bar_height);
    preX -= BAR_GAP;
}
```

## The Rest

But I had a working version. I'm missing about half the spectrum - the bass - if you compare it to a Monstercat video, but it works well enough. Most of the work left is to just pore through the sound library Minim's documentation to look for the correct functions to use to get the lower half of the spectrum. Then maybe refactoring some of the code for processing the values before being drawn. But! Here is the (half) working version in high quality and 60 fps, for a part of the song:

<iframe width="560" height="315" src="https://www.youtube.com/embed/5qB2VDdLEVU?si=4P5UYPzMDToznWX-" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

The source code is available on [GitHub](https://github.com/lohchness/music-visualizer).

So how is audio encoded digitally?

## How sound is encoded digitally

Who fuckin knows. # TODO: Expand here