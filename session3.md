# Session 3: Coordinate systems

## Introduction
 - This session is about 2D graphics
 - More specifically it's about 2D graphics under the hood
 - It's also about how we use 2D graphics to visualise and explore information and concepts
 - We're going to start by understanding how to visualise some of the sounds we've made 
 - Then we're going to try and do similar things but just using 2D graphics
 - This will mean using functions and expressions to create curves
 - We'll be using lots of for loops this session
 
## Visualising Sound waves
 - We can visualise wave forms very easily with maximilian
 - We do this by grabbing the audio buffer and writing it to an array
 - We can then create a draw loop and use the buffer output to draw lines of different lengths for each amplitude value
 - Each time the buffer changes, we get a new frame of audio values
 - The different line lengths correspond to the amplitude of the signal described by each value in the buffer.
 
 # Check it out:
 https://mimicproject.com/code/9e2e7a7f-e1b9-8606-a48b-f50428596cb8
 
## Coordinate systems
 - Here, we've been using a rectangular (or cartesian) coordinate system
 - This is the system we usually use for drawing when we start out
 - https://en.wikipedia.org/wiki/Cartesian_coordinate_system
 - It's important to realise that there are other types of coordinate systems
 - We need these to do anything other than draw straight lines.
 
## Drawing Circles
 - When you call the ellipse function in processing, or use the arc function on the JS Canvas the computer runs a function 
 - That function takes a position value for the centre of the circle (the origin), and a radius (distance from the origin)
 - It uses these two values to draw the circle using trigonometry. 
 - We can do this ourselves using polar to cartesian conversion
 - Here's an example:
 - https://mimicproject.com/code/44f2f678-dfb3-781b-dfa6-860aa56fceb5
 
## Polar to Cartesian Conversion (POLTOCAR)
 - In order to draw polar systems, we need to convert from polar to cartesian coordinates
 - We do this as follows:
 - x = (r * cos( θ ))
 - y = (r * sin( θ ))
 - θ is the angle in radians (we often call this 'theta', or 'phase')
 - r is the radius (or magnitude, or amplitude)
 - sin and cos are the mathematical functions we use to create curves
 - Together they allow us to work out where x and y are when we are thinking about angles and distances.
 - It's almost ALWAYS a good idea to think about angles and distances, and we'll be returning to this idea all the time
 
## Radius
 - The radius / magnitude is the distance from the origin
 - We can use to scale polar coordinates easily
 - This is because the angle contains the direction of travel 
 
## Getting the Radius back - CARTOPOL
 - We can use Pythagoras’ theorem to convert cartesian coordinates to a radius
 - This is because the radius (magnitude) is the length of the hypotenuse from the origin to (x,y)
 - This is also incredibly useful for finding out how far away you are from something
 
## CARTOPOL Theta
 - Getting the angle is more complicated - but very useful, as it represents the direction from the origin in radians
 - tan( θ ) = y / x So
 - θ = tan-1 ( 5 / 12 )
 - tan-1 is atan() - the inverse tangent
 - So the angle in radians = atan(y/x) for positive nonzero numbers
 - atan2 is used for all four quadrants of a cartesian coordinate space and cases where x=0
 - This is a bit tricky but we will come back to it all the time.

## Circles

 - Let’s return to our circle code
 - spacing is the distance around the circle
 - x = cos(spacing*n)*a
 - y = sin(spacing*n)*b
 
## Drawing polar waveforms
  - We can use this approach to draw the audio waveforms around a circle instead of in a line across the screen
  - We do this in the same way, but instead of joining up points around the circle, we draw lines of different lengths
  - The lines are spaced around the circle
  - The length of the lines is the amplitude of the value in the array
  - https://mimicproject.com/code/a7e2f833-49c8-d71f-99bd-19a993321e7e
  
# Exercise 
 - Take a look at this example. We use processing to create interesting shapes - I'll explain more about them later.
 - https://mimicproject.com/code/17134a36-adbd-d602-8947-dcfb87cec39b
 - Convert these processing examples so that they work in pure JavaScript
 - We're doing this to make you think about the actual algorithm
 

  
 
