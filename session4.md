# Session 4: Pixel Manipulation and Image Processing

![Mandala Image from Wikimedia commons](https://upload.wikimedia.org/wikipedia/commons/9/9a/Mandala_52.svg)

# Part One : Recap and Homework Review

## Recap
 - Last session we looked at basic 2D graphics concepts
 - We looked at simple canvas drawing functions and how we can use them to graph functions
 - We learned about cartesian and polar coordinate systems
 - We also looked at how to convert between polar and cartesian coordinates (super important)
 - We learned how to draw circles from scratch using trigonometry, and how this can be used as a basis for understanding how to create different kinds of curves
 - We learned about how the radius of a circle can describe the magnitude of something and also the distance between things
 - We also thought a little about how this is the same as calculating the hypoteneuse of a right-angled triangle, and is also the l2Norm / Euclidean Distance 
 - We looked at how the position around a circle is an angle in radians, which we can call Theta, or Phase, depending on what we're thinking about
 - We then looked at how we can use this knowledge to visualise periodic signals in polar space
 - We learned about how early computer graphics pioneers such as John Whitney used these approaches to create the first 2D and 3D computer graphics systems, and how these stylistically related to early abstract cinema and classical geometry.
 - I then set you all a task to take a more complex variant of this form called *Flores Geometrici*, and use it as a starting point to create your own interactive (or *reactive*) 2D asbtract artwork.

## Homework Review
 - Let's have a look at the work you have done in the last week. 
 - Break in to groups and discuss each others work. Then we'll come back together and look at some examples :-)
 - Do you have any questions about the task? What problems did you have?
 - To what extend do the works you created have the appearance of a Mandala? What is a Mandala?
  - How do these forms reflect on and inflect Hindu, Bhuddist and Islamic art forms?

# Part Two : Using Expressions to Fill Space

* This session is designed to reinforce core knowledge of pixels whilst additionally demonstrating under-the-hood examples for carrying out common pixel manipulation tasks. This includes:
 - Pixel representations - how pixel information is stored and represented, including colours
 - Pixel manipulation - how we can create both simple and complex shapes and textures using mathematical expressions 

## Creating Images From Scratch
 - The algorithms we used for creating the polar line drawings are basic geometric 'expressions' 
 - We're now going to learn about how we can draw filled shapes using similar expressions
 - For example, take a look at this:
 - https://mimicproject.com/code/f3a32c49-7c24-556f-af1b-91315be36ad9
 - The above example uses the 'createImageData()' method to draw some concentric rings.
 - We iterate through every pixels on the canvas
 - We then decide what colour each pixel should be by using a simple expression
 
## Writing output pixels
 - set red, green, blue, and alpha:
```JavaScript
position=(x+y*imageData.width)*4;
imageData.data[position] = c%255;
imageData.data[position+1] = c%255;
imageData.data[position+2] = c%255
imageData.data[position+3] = 255;
```
 - The modulo operator is to ensure that the output never goes over 255, which is the maximum colour value
 - The 'position' line moves through the Image Data 'array', writing colour channels for each position.
 - It's going to take a while for you to get familiar with this code - BUT YOU NEED TO.
 
 ## Another simple expression
  - https://mimicproject.com/code/bfcbcefb-ba11-f96b-21f5-7a6629ee7e61
  - This algorithm uses trigonometric functions across both X and Y
  - Spend some time using what you learned last week to create a new expression. 
  - Don't be scared to experiment!
  
 ## Create your own simple expression
  - Spend some time in groups attempting to generate new expressions
  - Consider using trigonometric approaches.
  - **Can you add new terms and/or mathematical functions, for example sin, cos, tan, atan, abs?**
  - **Could you incorporate conditionals to specify different parts of the screen?**
  - **Could you run more than one loop?**
  
  
# Part Three : Lecture 

- This lecture provides more detail on image processing, including:
 - Manipulating existing images by using combinations of loops, conditionals and Math 
 - 2D Image convolution - how we can use a convolution 'kernel' to create a range of image filters

## Review: Pixel Formats
- In JavaScript, pixels are held in imageData buffers
- As we've seen we can write values directly in to imageData buffer arrays 
- You probably noticed that these are actually one-dimensional arrays, so we don't technically need to think about them as rectangular images
- However, it is actually much more useful if we do. We use nested for loops to help us access and create data as columns and rows
- One thing that makes everything extra tricky is that each pixel position (i,j) actually has **4** values in the array that it needs in order to create the pixel
- These four values are the **RED, GREEN, BLUE and ALPHA** channel colour values
- Each value is an 8-bit value, meaning that each pixel is represented by 32 bits of information (8 bits per channel).
- This means that when we are trying to process imageData arrays, to get to pixel (50,10) of a 100 * 100 image, we actually need to get to array value **((50 * 100) +10) 4**. At that point, we will then find 4 values - the actual RGBA data for that pixel.
- As a formula, where w is the imageWidth, j is the x coordinate, and i is the y coordinate, this is `((y*imageWidth)+x)*colourChannels`
- So the code you would need to access this pixel in JavaScript is actually:
`imageData.data[((50 * 100)+10) * 4];`
- Remember, on many platforms / different languages, pixel data isn't in RGBA format. In JavaScript though, it most always is, but it's actually your job to know so make sure you do. It really matters.
- We use nested for loops to make accessing the pixel data easier. We can treat `i` as the column variable (the `y` axis value). We can then cycle through all the row values, usually referred to as `j` (the `x` axis values) at that column position.
- We do this by multiplying `i` by the image width (which gives us one whole row for each `i`), then adding the current row pixel value j (the `x` value).
- Finally, to account for the fact that the actual size of the array is 4 times the image dimensions, we multiply by 4. This will land us on the RED pixel value for that `(i,j)` coordinate - like this:
`imageData.data[((imageWidth * i) + j) * 4] = 255; // set the RED pixel at i to its maximum value of 255`
- Finally, to access the Blue colour value you would need to do this:
`imageData.data[((imageWidth * i) + j) * 4 + 2] = 255; // set the Blue pixel at i to its maximum value of 255`
- This is because the position in the pixel array + 1 is Green, +2 is Blue, and +3 is Alpha.

 ## Basic Image Processing
  - We can load an image and perform basic operations in order to alter it
  - We can use 'getImageData()' to do this
  - In the below example, we use the > operator to threshold the image
  - https://mimicproject.com/code/6f02256b-bd70-e782-054b-435ad3ac8eaa
  - You might need to press 'play' to get the image to load.
 - This example is a threshold.
  - What else could we do?
  - Could we invert the threshold? What would this do?
  - How could we increase the brightness?
  - How could we increase the contrast?
  - Are there better ways of doing this?
  - Well yes of course. For example, we can generate brightness by interpolating the current pixel value against 0. We could generate contrast by interpolating the current pixel value against gray (which is sort of what we did). Finally, we could create saturation by interpolating the current pixel value against it's own luminance. You can generate luminance very easily with the following formula: 
  `(0.2126*R + 0.7152*G + 0.0722*B)`.
  - Once you have this value for the pixel, you could interpolate a new value by doing something like this:
 `(1 – saturation_value) * pixel_luminance + saturation_value * actual_pixel_value` 
  - This is extremely similar to what we did when we interpolated new values for changing the speed of audio sample playback. 
  
 ## Rotating an Image the Hard Way
  - In most Creative Coding frameworks you can just call 'rotate' to rotate an image.
  - But it's worthwhile taking a look at how this actually works
  - The below example shows how we can use something similar to the circle formula from last week to rotate each pixel to a new location on the screen.
  - https://mimicproject.com/code/86c8ecc8-4fb7-a25b-448d-a05e3fb4b6ed
  - There are two important parts to this code. First we need to calculate which pixel we want to move, and use a 2D rotation to move it.
```JavaScript 
// This is a 2D matrix rotation!!! It's very similar to the code we used to rotate points around a circle.
var x = Math.floor((Math.cos(theta) * j) - (Math.sin(theta) * i));
var y = Math.floor((Math.sin(theta) * j) + (Math.cos(theta) * i));
```
 - j is the current pixel's original Y position, i is the current pixel's original X position.
 - j and i here are acting like the radius of the circle
 - theta is the angle, or how far round the circle we want to rotate 
 - We use Math.floor to round down, as this is an actual pixel xy coordinate. If we don't do this, things could get messy
 - The two new vars, x and y, are going to be where we are copying from - we want these colour values to be written to the current pixel
 - The next bit of code does that part:
```JavaScript  
imageData2.data[((imageWidth * i) + j) * 4] = data[((imageWidth * y) + x) * 4];
```
 - We are using the rotation code to work out which pixel we actual want to write in to the imageData buffer at that point. This means we need to calculate a rotation for every i j, and write the pixel values - all four of them (RGBA) from where they are, back to where we want them! 
 
 ## Additional Materials: Rotation Code with Zooming, Offsets and Anchors
 - People often aske how to change the origin of a rotation.
 - To do this, you need to make adjustments to the Matrix rotation.
 - We are adding parameters to translate the origin, translate the image, and scale (zoom) the image.
 - Below is the code with the important changes:
 ```JavaScript 

// Rotation, translate (offset), origin translate (anchor) and scale (zoom)

var x = Math.floor((Math.cos(theta)/zoomX) * (j-(offsetX+anchorX)) - (Math.sin(theta)/zoomY) * (i-(offsetY+anchorY)))+anchorX;
var y = Math.floor((Math.sin(theta)/zoomX) * (j-(offsetX+anchorX)) + (Math.cos(theta)/zoomY) * (i-(offsetY+anchorY)))+anchorY;
```
 - Here's a link to a document with the above included:
 - https://mimicproject.com/code/e9d8b9db-7e79-8aaa-9ec2-e672cd76eaa9 

 
 ## Image Processing using Convolution
  - We can produce a wide range of image processing effects with a process called 'convolution'
  - Convolution allows us to perform blurs, edge detections and other common filter processes
  - To do this, we create what is called a 'kernel', which is a small grid of numbers, 3 * 3 for example.
  - The kernel decides what the central output pixel should be by multiplying the surrounding pixels by values in the grid
  - After the multiplications, all the values get added together and averaged to find the value for the centre pixel.
  - The below is an excellent visual explanation of image kernels. 
  - http://setosa.io/ev/image-kernels/
  - There are even more here:
  - http://aishack.in/tutorials/image-convolution-examples/
  
## Performing an Edge Detection / Gradient analysis
  - Here's an example that uses the simplest possible approach to perform an edge detection
  - This edge detection is very efficient and actually very powerful
  - https://mimicproject.com/code/e9e74da1-ecd7-719d-9c8c-51d5b52d4cad
  - (remember to press the play button if the images don't appear)
  - The example uses a very very simple image processing approach which is operating in place, rather than as a separate array
  - So we're taking a short-cut (no convolution kernel, just manual multiplication of pixels)
  - It uses a 'kernel' of -1 0 1 in **only one dimension**. You can select either the X or Y dimension to see the effect.
  - This produces a basic edge detection - but it can do much much more than this.

`imageData2.data[((imageWidth * i) + j) * 4] = (-1*(data[((imageWidth * i) + j-1) * 4])) + (data[((imageWidth * i) + j+1) * 4]);`

 - The above code takes the pixel before the current position, and multiplies it by -1, which inverts it (so 128 would become -128). 
 - It then takes the pixel **after** the current pixel (e.g. 128) and adds it (it ignores the data in the current pixel entirely).
 - This gives you a new image which only contains **the difference between the previous pixel and the next pixel**
 - In the above example, the output pixel value would be 0. This would mean that **nothing in the image had changed at that point**
 - This produces what we call `gradients`
 - These can be used to create edge detection, but frankly, the gradients are much more powerful than that.
 
 
## What you can do with Gradients
 - The gradients are either across X or Y, and are the basis of simple computer vision approaches
 - They tell you where the most change occurs in the image, with pixels representing where the greatest differences are between parts of the image
 - If you get two image buffers, one with the X gradients, and one with the Y gradients, you can then do some cool things
 - For example, you can run through all the gradients performing a cartesian to polar conversion on the average of groups of pixel gradients
 - This can tell you what the magnitude and direction of the gradients are at those points.
 - You can use this information to spot things in images, for example, the characteristic curves of the human body and face.
 
  
## HOMEWORK
 - You have a choice between two different exercises. I don't care which one you do.
 - 1) Try to understand how the edge detection code works, and use this knowledge to create a blur effect
 - It's a simplified convolution kernel but can be used to create basic blurs.
 - OR
 - 2) Take a look at this example:
 - https://mimicproject.com/code/95b09168-00c1-b781-1cf1-9ba3761c276d
 - Write 1000 words on this example, explaining it in as much detail as you can
 - The comments should help a great deal, but you should make sure to explain it in your own words!
