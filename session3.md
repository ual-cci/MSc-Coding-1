# Session 3: 2D Graphics Part One: Graphs, Shapes and Coordinates

![Still taken from Will Gallia's 'Adventures in Sine](http://www.wgallia.com/content/images/ais/sine1.jpg)

Still Taken from Will Gallia's "Adventures In Sine", http://www.wgallia.com/content/images/ais/

## Introduction
 - This session is about 2D graphics
 - More specifically it's about 2D graphics under the hood
 - It's also about how we use 2D graphics to visualise and explore information, concepts and visual experiences
 - We're going to start by understanding how to visualise some of the sounds we've made 
 - We're going to look at different ways you can plot waveforms in 2D and think about how we explore these creatively
 - We're going to try and create simple visual synthesisers using the same approaches, but in 2 Dimensions
 - This will mean using functions and expressions to create curves in space
 - We'll also think about how these curves in space can be thought of as representing different kinds of information or experiences
 - In terms of programming skills, we'll be using the js canvas quite a bit today
 - We will also be using for loops to create simple visual algorithms

# Part 1: Recap of Last Session

## Understanding Samples and how they work

- Last session we learned how 1D audio data is represented in a computer system
- We thought about how microphones work, and how they convert acoustic vibration in to variations in an electromagnetic field
- We also refreshed our knowledge of how these field variations can be measured by a computer as lists of numbers.
- We looked at lists of 16bit values and graphed them, and considered what happens when we push them through a speaker at different speeds
- (although we glossed over how Analogue to Digital and Digital to Analogue Converters work)
- We also considered how *anything* - not just representations of acoustic waves in an electromagnetic field expressed as lists of numbers - can be sonified.

## Sample Interpolation
- We learned that you can manipulate the playback speed of samples, thus changing the perceived pitch and duration of the waveforms they represent
- We also thought about the fact that we need to make up new sample values when we change the plaback rate, through a process called 'interpolation'
- We looked at a few different types of interpolation, including linear and cubic interpolation, and talked about how they work 
- Finally, we learned that you can just use the maxiSample object to save you from all this pain.

## Loading and Controlling Samples
- We used maxiSample to load and play back samples
- We used oscillators to modulate the playback speed of samples
- We also explored how you can play back samples in reverse by running through the list of numbers backwards (interpolating in reverse as we go!)

## Triggering Precise Events Using maxiClock
- We learned that we can use oscillators to create simple, sample accurate clock mechanisms
- I introduced you to maxiClock, which is basically an oscillator-driven clock machanisms with some slightly more intuitive controls.
- We learned how to set the tempo in Beats Per Minute, how to set the number of 'ticks' per beat, and how to use these values to make things happen at specific times
- We looked at how we can use conditionals to test for specific situations, and make creative decisions based on these
- I then asked you to use these methods to create some simple sound-based systems as part of your homework :-)

# Homework Review
## Let's spend some time reviewing the homework before we continue!

 
# Part 2: Visualising Sound waves
  
 ## Let's take another look at the visualisation code we've been using:
 https://mimicproject.com/code/9e2e7a7f-e1b9-8606-a48b-f50428596cb8
 - We can visualise wave forms very easily with maximilian
 - We do this by grabbing the audio buffer and writing it to an array
 - We can then create a draw loop and use the buffer output to draw lines of different lengths for each amplitude value
 - Each time the buffer changes, we get a new frame of audio values
 - The different line lengths correspond to the amplitude of the signal described by each value in the buffer.

## Analysing the draw code
- So we know we're going to take each value in the list and use it to create a line
- And the length of the line is based on the size of the value in the audio buffer
- So each frame is a visualisation of each audio buffer
- The reason it appears stationary (isn't moving around) is that we have locked the audio waveform duration to the number of values in each buffer
- We are then dividing up the width of the screen by the number of values in each audio buffer
- This is the default value - 1024. 

`        var spacing = (width / 1024);
`
- Then we equally space each line across the screen using a for loop

```javascript
           
           for (var i = 0; i < 1024; i++) {
                context.beginPath();
                context.moveTo(i * spacing, height / 2);
                context.lineTo(i * spacing, height / 2 + (drawOutput[i] * height / 4));
                context.stroke();
                context.closePath();
            }
```

## Coordinates
 - Here, we've been using a rectangular (or cartesian) coordinate system
 - This is the system we usually use for drawing when we start out
 - https://en.wikipedia.org/wiki/Cartesian_coordinate_system
 - It's important to realise that there are other types of coordinate systems
 - We need these to do anything other than draw straight lines.
 - Today, we are going to be drawing lots of curves. To do this, we need to use a very different 2D representation called a **Polar Coordinate System**

# John Whitney Senior

- John Whitney Senior is a key figure in computer graphics
- He was originally a composer who used a number of techniques to create experimental music and video art
- Some of his earliest computer graphics work was completed on discarded M5 and M7 targetting computers
- This led to him creating the first computer generated title sequence in 1957

https://www.youtube.com/watch?v=4CZfSc6nJ8U

- Here's an interesting online article on the topic with some photographs of the device he used:
https://www.diyphotography.net/alfred-hitchcocks-vertigo-possibly-first-movie-use-computer-animation/

- He and his brother James won a prize at the world's first experimental film festival for a series of works they created in 1944 entitled *Five Abstract Film Exercises*.
- This link is film number 4 from that series. The images are created with pantographs, and the audio is additive synthesis plotted on graph paper, and drawn on to the soundtrack using modified pendulums.

https://www.youtube.com/watch?v=nTEABxz1e_k

In 1961, John Whitney produced this film, which is a Catalogue of artworks comprising some of the world's first computer animation.
https://www.youtube.com/watch?v=TbV7loKp69s

This is a fascinating film where John Whitney explains his early computer graphics experiments at IBM
https://www.youtube.com/watch?v=jIv-EcX9tUs


https://mimicproject.com/code/a1996d3f-ecf1-75ae-5486-30904042bfcc

# Part 3  
 
## Using Polar Coordinates
- Usually when we draw circles, we call a function to do so
- e.g. we can use the canvas `arc` function, or the p5 `circle` or `ellipse` functions 
 - When you call the ellipse function in processing, or use the arc function on the JS Canvas the computer runs a function 
 - That function takes a position value for the centre of the circle (the origin), and a radius (distance from the origin)
 - It uses these two values to draw the circle using trigonometry. 
 - We can do this ourselves using polar to cartesian conversion
 - Here's an example:
 - https://mimicproject.com/code/44f2f678-dfb3-781b-dfa6-860aa56fceb5
 
## Polar to Cartesian Conversion (POLTOCAR)
 - In order to draw polar systems, we need to convert from polar to cartesian coordinates
 - We do this as follows:
 - `x = (r * cos( θ ))`
 - `y = (r * sin( θ ))`
 - θ is the angle in radians (we often call this 'theta', or 'phase')
 - r is the radius (or magnitude, or amplitude)
 - sin and cos are the mathematical functions we use to create curves
 - Together they allow us to work out where x and y are when we are thinking about angles and distances.
 - It's almost ALWAYS a good idea to think about angles and distances, and we'll be returning to this idea all the time
 - When the radius is equal to 1, we think of the circumference of the circle is `TWO * PI` (`2PI` or `TWOPI` or `2 * 3.14159` or just `6.28318`).
 - This means if we know how many segments we want to use to divide up the circle, we can divide TWOPI
 
## Radius
 - The radius / magnitude is the distance from the origin (the centre)
 - We can use this to scale coordinates easily
 - This is because the angle contains the direction of travel
 - When we multiply the angle by the radius, the point we are drawing moves further away from the centre
 - It does this in the direction described by the angle
 - When we convert from polar coordinates back to cartesian coordinates, the angle is contained in both the x and y coordinate.
 - This is why when we multiply both x and y coordinate of a point, it increases in magnitude, and this magnitude is equal to the radius.
 
## Getting the Radius back - CARTOPOL
 - We can use Pythagoras’ theorem to convert cartesian coordinates to a radius
 - This is because the radius (magnitude) is the length of the hypotenuse from the origin to (x,y)
 - This is also incredibly useful for finding out how far away you are from something
 - I'm sure you remember this from High School:
 
 ![pythagoras theorem (creative commons license)](https://upload.wikimedia.org/wikipedia/commons/9/9e/Pythagoras-proof-anim.svg)
 
 
## CARTOPOL Theta
 - Getting the angle is more complicated - but very useful, as it represents the direction from the origin
 - tan( θ ) = y / x So
 - θ = tan-1 ( y / x )
 - tan-1 is atan() - the inverse tangent
 - So the angle in radians = atan(y/x) for positive nonzero numbers
 - atan2 is used for all four quadrants of a cartesian coordinate space and cases where x=0
 - This is a bit tricky but we will come back to it all the time.

## Circles

 - Let’s return to our circle code
 - spacing is the distance around the circle
 - x = cos(spacing*n)*a
 - y = sin(spacing*n)*b

## Drawing Polar Graphs of Waveforms
  - We can use this approach to draw the audio waveforms around a circle instead of in a line across the screen
  - We do this in the same way, but instead of joining up points around the circle, we draw lines of different lengths
  - The lines are spaced around the circle
  - They are drawn from the centre of the circle (amplitude = 0) to the edge (maximum amplitude)
  - When we do this, we can see the phase wrapped around the c
  - The length of the lines is the amplitude of the value in the array
  - https://mimicproject.com/code/a7e2f833-49c8-d71f-99bd-19a993321e7e
  

## Synthesising 2D Waveform Graphs Directly
- Let's build a simple system for creating polar curves without audio
- This is a simple form of one of John Whitney's favorite algorithms, which he referred to as *The Roses of Grandii*
- The original curve was created by Luiugi Guido Grandii in 1728. It's called *Flores geometrici* and is very well known
- You can find plenty of examples of Flores geometrici on the web in fairly complex form.
- There's quite a boring article on the algorithm on Mathematica.
https://mathworld.wolfram.com/Rose.html
- The version we are going to create is the basic curve as described above.

- Here's most of the code...
```javascript

  let canvas = document.querySelector("canvas");
  let context = canvas.getContext("2d");
  canvas.width = 800;
  canvas.height = 600;
  
  var radius = 100;
  var penSize = 5;
  var positionX = 200
  
  var draw = function() {

    for (var i = 0; i<500; i++) {

    context.fillRect(positionX+Math.cos(i*Math.sin(i))*radius,positionX+ Math.sin(i *Math.sin(i))*radius,penSize,penSize);
    }
    requestAnimationFrame(draw);
    
  }
  
  requestAnimationFrame(draw);
  ```

# Session 3 Homework

- Here's a slightly more developed version of *Flores geometrici* that uses the mouse to control the formation of the petals
- https://mimicproject.com/code/a1996d3f-ecf1-75ae-5486-30904042bfcc
- Notice that this one calculates the spacing around the circle and uses this as a parameter to create harmonics, similar to those we saw in the audio visualisation
- For homework, I want you to make an interactive artwork using this algorithm as a starting point
- You might want to take Will Gallia's *Adventures in Sine* as an inspiration, or some of the John Whitney work.
- Don't shy away from using colour
- Consider drawing other shapes at the different positions, and not just straight lines.
- Consider using dynamics - can you use the loop parameters (e.g. i) to change the size, shape, colour etc.? 
- Can you use conditionals to make the output even more interesting and dynamic?

  
 
