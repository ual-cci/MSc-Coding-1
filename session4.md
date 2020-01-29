# Session 4: Pixel Manipulation and Image Processing

## Recap
 - Last session we looked at basic 2D graphics concepts
 - We learned about cartesian and polar coordinate systems
 - We also looked at how to convert between polar and cartesian coordinates (super important)
 - We learned how to draw circles from scratch using trigonometry
 - We learned about how the radius of a circle can describe the magnitude of something and also the distance between some things
 - We also thought a little about how this is the same as the hypoteneuse of a right-angled triangle
 - We learned about how the position around a circle is an angle in radians, which we can call Theta, or Phase, depending on what we're thinking about
 - We then looked at how we can use this knowledge to visualise periodic signals in polar space
 - I then set a task for you to all convert a simple processing sketch that draws interesting polar patterns so that it runs in pure JavaScript

## First
 - Let's have a look at the work you have done in the last week. 
 - Do you have any questions about the task? What problems did you have?

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
  
 ## Basic Image Processing
  - We can load an image and perform basic operations in order to alter it
  - We can use 'getImageData()' to do this
  - In the below example, we use the > operator to threshold the image
  - https://mimicproject.com/code/6f02256b-bd70-e782-054b-435ad3ac8eaa
  - You might need to press 'play' to get the image to load.
  - What else could we do?
  
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
 - Note that we could do it the other way round. We get a very similar effect but with some different artefacts
 
 ## Image Convolution
  - We can produce a wide range of image processing effects with a process called 'convolution'
  - Convolution allows us to perform blurs, edge detections and other common filter processes
  - To do this, we create what is called a 'kernel', which is a small grid of numbers, 3 * 3 for example.
  - The kernel decides what the central output pixel should be by multiplying the surrounding pixels by values in the grid
  - After the multiplications, all the values get added together and averaged to find the value for the centre pixel.
  - http://setosa.io/ev/image-kernels/
  - http://aishack.in/tutorials/image-convolution-examples/
  
## Performing an Edge Detection
  - Here's an example that uses an even simpler approach to perform an edge detection.
  - This edge detection is very efficient and actually very powerful
  - https://mimicproject.com/code/e9e74da1-ecd7-719d-9c8c-51d5b52d4cad
  - (remember to press the play button if the images don't appear)
  
## HOMEWORK
 - You have a choice between two different exercises. I don't care which one you do.
 - 1) Try to understand how the edge detection code works, and use this knowledge to create a blur effect
 - It's a simplified convolution kernel but can be used to create basic blurs.
 - OR
 - 2) Take a look at this example:
 - https://mimicproject.com/code/95b09168-00c1-b781-1cf1-9ba3761c276d
 - Write 1000 words on this example, explaining it in as much detail as you can
 - The comments should help a great deal, but you should make sure to explain it in your own words!

## Additional Materials: Rotation Code with Zooming, Offsets and Anchors
 - Quite a few of you asked how to change the origin.
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
