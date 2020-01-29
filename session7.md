# Session 7: GLSL Shaders Part 1

## Introduction to GLSL using Fragment Shaders

* You now know how to build basic 3D worlds using GL.
* However, you may have also noticed that GL can be a little restrictive
* For example, dynamic systems are difficult to code.

---

## Going Deeper, Doing it better

* To do this properly, you really need to use shaders.
* Shaders are absolutely nuts.
* No seriously, they are the most fun thing your computer can do.
* Don't believe me? Check out these links:

- https://www.shadertoy.com
- http://www.shaderific.com/glsl-functions/
- https://thebookofshaders.com
- http://glslsandbox.com (sometimes a bit sketchy so be wary)

---

## Presentation:

Grab the PDF presentation here:

- https://github.com/micknoise/Advanced-Creative-Coding-1/blob/master/Session-7-part1.pdf

---

## Exercise 1

* Log in to mimicproject.com.

* Go to the following document and fork it:

https://mimicproject.com/code/e2fb6d1d-e5f8-a950-5119-b47535a82752

This page has lots of code on it. The majority of it is management code to set up the shaders. You can ignore this for now.

At the moment you only need to focus on the code within the section marked "PUT YOUR GLSL CODE HERE".

* Referring to the lecture slides, try to modify the colours of the fragment shader by using the time uniform and a mathematical function.

* Try to memorise the GLSL code (JUST the GLSL section after the part marked "PUT YOUR GLSL CODE HERE" and before the part marked "END OF GLSL CODE")

* Next, fork this document:

https://mimicproject.com/code/3dd25d78-374d-2826-a569-9400ae357ac2

* Uncomment the line which uses the distance field to form a circle. How does it work?

* Try to use the 'smoothstep' function to make the edges of the circle smooth.

* Now try to change the position of the circle by multiplying the centre of the circle by the mouse position.

* Can you change the colour of the circle based on the y dimension? Make a note of the effect this has.

* Look at this method instead: https://mimicproject.com/code/ff025d22-ab74-dccd-2e0e-55b8bc6cdb60

What is the main difference? Does it matter?

Uncomment the line which contains the modulo function. Comment out the other pos2 line as indicated in the code. What is going on here?

Take a longer look at these examples..

https://mimicproject.com/code/94d49eac-8925-fcee-0046-8bd6a9509f10

https://mimicproject.com/code/67d64682-a09f-8d50-c60f-206c1addc9ba

https://mimicproject.com/code/3c30839f-92e0-8443-3cd9-1a91e8ef2b5f

---

## Presentation (continued)

Next, we need to look at the following presentation:

- https://github.com/micknoise/Advanced-Creative-Coding-1/blob/master/session7-part2.pdf

---

## Exercise 2

Go to the following document and fork it:

https://mimicproject.com/code/ba6a2bbd-dd43-e661-da51-ec36fccbc0d3

Here you can see a series of functions for creating squares and circles (Remember we're just working on the fragshader code)

You should notice that the square functions create squares, not rectangles.

* Create a new called rectangle that lets you specify the length of the sides independently.

Now try to create a simple picture with lots of rectangles, squares or circles of different colours. Remember you can add, subtract or multiply the outputs of functions. Make notes about the kinds of effects this can have.

* If you are feeling brave, use a mat2 matrix to skew the sides of the square, or to rotate it. You can copy the rotation matrix from this code:

https://mimicproject.com/code/ef644559-9ad7-0e8a-b32b-2fbd7da69db1

* Fork this document:

https://mimicproject.com/code/0e84f212-142e-8cef-b427-fa1d8492f368

It shows you how to create lines.

* Do a complex line drawing using a sequence of lines that carry out specific functions.

Try to create expressions with combinations of sin, cos, tan, atan, pow etc. Look up the functions on shaderific for some inspiration.

* Experiment adding and subtracting the lines together. Remember that when you combine functions together, every pixel can be affected.

* Now fork this document.

https://mimicproject.com/code/8028d479-ec2f-e8ca-0bc8-891a4669d66f

This document has a vertex shader. Experiment with it to try to work out what it's doing. Can you create simple algorithmic geometry in this shader?

---
