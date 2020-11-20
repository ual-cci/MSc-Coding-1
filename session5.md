# Session 5: 3D Graphics From Scratch

# Part One : Recap
 - Last session we looked at more advanced 2D graphics concepts
 - We used expressions to create complex pixel manipulations
 - We also learned about how to do basic image processing
 - We looked at concepts such as convolution for edge detection, bluring, and other effects
 - Some of us also thought about complex space a little, and looked at the mandelbrot set a bit...

## Homework Review
 - Let's have a look at the work you have done in the last week
 - In your groups, discuss what you did. If you created a filter, share it. If you wrote about fractal, share this too.
 - Come up with some questions we can discuss - What problems did you have? What isn't clear? Help each other!

# Part Two : 3D Graphics Systems From Scratch

This session will take us through how to create a basic 3D graphics engine using a simple 2D drawing context. You might have guessed a little how we might approach this, but by the end of this session you should have a much better idea of how a 3D graphics system produces images with a sense of depth and perspective.  

## Let's start at the very beginning.

https://www.youtube.com/watch?v=yMeSw00n3Ac

- This is the very first 3D computer graphics sequence in any major movie.
- It was produced by the artists Larry Cuba. 
- Larry Cuba worked with John Whitney, and is a hugely important figure in experimental cinema *and* computer graphics
- Shout out to Larry in case he's reading :-) We love you.

## First Principles
- In order to draw a 3D scene, we need to create the illusion of depth.
- We do this by introducing the idea of a perspective *projection*
- What this means is, we take 3D coordinates, and we use a simple algorithm to determine 

## 3D Perspective Projection
- We're going to talk through the code for a simple perspective projection
- The starter code for this is here:
- https://mimicproject.com/code/d2e93d74-8a13-0d7c-6e06-68048f433b4c
- In the example code we create a bunch of random coordinates
- These are 3D vectors, which we call vertices. Each individual vector is called a vertex.
- We do this in 3D, which means we create an x, y and also z coordinate for each vertex
- The z coordinate tells us how far the vertex is away from the us - i.e the *perspective camera*

## Small, or Far Away? 

- As things come towards us, we make them bigger, so we can use this value to scale any objects that we draw at the vertex positions.
- https://www.youtube.com/watch?v=MMiKyfd6hA0
- This is a good start, but something else also happens when things come towards us
- As they move approach, they have the appearance of moving further to our left or right, or above or below us.
- This depends on the direction of the vertex in relation to the origin (the centre of the world as we look at it)
- The vertex moves further away from the origin in the same direction as it approaches us 
- We simulate this by scaling the x and y coordinates as the z coordinate increases

## Field of View
- We could just use the z coordinate to directly scale the x and y values, as well as the size of the point we will draw
- However, this really doesn't work very well, and don't simulate real world experience as well as we might like
- In order to make this a bit better, we generate an intermediate value called a *Field of View*
- Field of view is basically a term that means 'what the camera can see', but it also describes the extent to which we understand size and distance in a visual scene.
- One simple way to emulate field of view mathematically to scale a vertex is to generate a value, add the z coordinate of the vertex, and divide by the starting value.
- This produces a factor that represents the ratio of the field of view to the vertex z position.
- There are other ways of doing this which are slightly better, but we will come on to those later.

## The Code:

- Here's the raw code which we will talk through in this section:
```JavaScript 

var canvas = document.querySelector("canvas");
var width = window.innerWidth;
var height = window.innerHeight;
var context = canvas.getContext("2d");
canvas.width = width;
canvas.height = height;

var fov = 200;
// This array is used to create an individual 3D vertex, represented by a 3D vector xyz
var point = [];
// This is where we stash all the vertices
var points = [];
  // This is temp storage for when we draw each 3D vertex
var point3d = [];

var HALF_WIDTH = width / 2;
var HALF_HEIGHT = height / 2;

var numPoints = 1000;
  // This is temp storage for all the individual vertex coordinates in the vector
var x3d = 0;
var y3d = 0;
var z3d = 0;

  // This generates a static random starfield.
for (var i = 0; i < numPoints; i++) {
  // randomly produce a number between 0 and 1
  // for each x, y and z coordinate
  // scale it (using width or height)
  // then centre it using width or hight
    point = [(Math.random() * width / 2) - width / 4, (Math.random() * height / 2) - height / 4, (Math.random() * width / 2) - width / 4];
  // add the vertex 
    points.push(point);
}

  // Now we draw the static random starfield
function draw() {
    
// This just clears the screen and paints it black  
    context.fillStyle = "rgb(0,0,0)";
    context.fillRect(0, 0, width, height);
// This loop takes a bunch of 3D vertices and draws them using a 2D perspective projection
    for (var i = 0; i < numPoints; i++) {
        
      	// Get a vertex
        point3d = points[i];

        // // Get the z coordinate - this is the depth
        z3d = point3d[2];
                
        // if the z coordinate for this vertex is beyond Fielf of View (FOV),
        // Add half the width to move it back. This makes an endless starfield.
        // feel free to disable this if you want...
        if (z3d < -fov) z3d += HALF_WIDTH;
        
        // replace the original z position with this new z position.    
        point3d[2] = z3d;
        
        // Now get all the coordinates in to separate values to make them easier to wrangle        
        x3d = point3d[0];
        y3d = point3d[1];
        z3d = point3d[2];
        
        // Decide on the size of the point by taking the FOV and dividing it by the FOV + the z pos
        var scale = fov / (fov + z3d);      
        // Now create the 2D perspective projection.
        // create a 2D x and y position by multiplying the x and y coordinates by the scale
        // Add half the width and height to translate the coordinates to the origin.
        var x2d = (x3d * scale) + HALF_WIDTH;
        var y2d = (y3d * scale) + HALF_HEIGHT;

        // Draw a square of size 'scale', in position x2d, y2d.

        context.fillStyle = "rgb(255,255,255)";
        context.fillRect(x2d, y2d,scale,scale);
  
        //That really is it...
        
    }
	requestAnimationFrame(draw);
}

	requestAnimationFrame(draw);



```

## Quick Exercise
- In groups, take a look at the code here:
https://mimicproject.com/code/d2e93d74-8a13-0d7c-6e06-68048f433b4c
- For some reason, it's not producing the perspective projection. 
- Fix the code !
- Once you've done this, take a look at these variations:
https://mimicproject.com/code/2451b558-27ab-93f6-4fa6-224c475d1e03
https://mimicproject.com/code/dcd998f4-9146-8b50-9218-9d09653d2f58

# Part Three : 3D Graphics In Depth

- This lecture will explain core mathematics concepts that we need to consider when working in 3D.
- There's quite a lot to take in, so I've made a presentation
- These have details of all the work required with this weeks session
- They include example code, and full explanations of core 3D graphics concepts, including an introduction to matrix transformations.
- https://ual-cci.github.io/mick/ACC-1-3D-graphics/3D%20graphics/

 or grab the zip here:

https://github.com/ual-cci/MSc-Coding-1/blob/master/3D%20graphics.zip 
  
## HOMEWORK
 - Start from the basic 3D perspective projection that we used.
 - Create an interactive geometry system using this basic engine.
 - Think about how you can adapt some of the knowledge you have learned in previous sessions
 - Also, consider how you might use distance as a factor.
 
