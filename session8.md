# Session 8: GLSL Shaders Part 2


---
## GLSL shaders continued

NOTE: This session is deprecated but may be useful for those who are interested in understanding more about GLSL shaders, specifically how to control lighting under the hood

Today we will be looking at noise generators for a little bit.

Then we will be looking at Vertex shaders in detail.

The main technical learning we are reinforcing are GLSL shader language operators (which are standard operators we have looked at before), and functions, because we need to use functions a lot in GLSL to simplify things.

If you are looking for the bump mapping example, you can find it here:

https://mimicproject.com/code/0d649cb7-0cca-a70a-86b2-f3e087402d12

---

# Part 1 - Recap and Homework Review

## Last Week's Session!

- Last week we learned about Fragment Shaders
- We learned that we can create Fragment shaders with GLSL
- We learned that GLSL is a great language with lots of amazing built in functions 
https://www.shaderific.com/
- We also learned that we have to think about everything differently because every fragment is rendered simultaneously
- We learned that GLSL is basically just like C - you can use C-like expressions, constructs etc., but it's much more powerful
- We learned that shaders are used to do High Performance Computing (HPC), for example, Machine Learning and AI, and other types of compute operations.
- We learned that gl_FragCoord and gl_FragColour are built in variables that we need to have in our fragment shader program
- We learned about Uniforms - what they are, how they work, how to set them up, and how to pass them between our main program and our shaders
- We created shapes of different kinds using algorithms and expressions, and also learned how to create lines. This was a bit weird for all sorts of reasons but also really cool.

- Finally we all made some creative work in a fragment shader using line functions and (possibly) shape functions.

## Homework review
- Let's share our stuff!!!

# Part 2 : Pseudorandom numbers in fragment shaders

- We'll be doing the first section (on pseudorandom functions) in class
- This stuff is pretty easy as we've already talked about most of it before
- But the context might make it seem more difficult - but don't worry, it isn't

# Part 3: Presentation:

Grab the PDF presentation here:

- https://github.com/ual-cci/MSc-Coding-1/blob/master/Session-8.pdf

- We'll be doing the second section (on vertex shaders and normals for procedural/dynamic geometry) in the video lecture
- You can do all the excerises as homework. They are not as hard as they first appear. Any questions, please feel free to message me.
- You should set aside 3-4 hours minimum to go through the exercises below after watching the lecture. Refer to your notes from the in-class talk, review the blackboard session, and use the lecture as your main resources. Everything you need to know is there :-)

---

# FINAL HOMEWORK !!!

## Exercise 1

Log in to mimicproject.com.

Go to the following document and fork it:

https://mimicproject.com/code/b127c4fb-e76f-76e1-09ab-18973a61eedd

Locate the randfm function.

Find where the function is called. Alter the frequency and amplitude. What happens to the patterns at high amplitude? Write a short paragraph describing your observations.

Can you work out why this is happening? Try to reason about the process and write it down. 

---

## Exercise 2

Now go to this document and fork it:

https://mimicproject.com/code/15f43bb8-fecb-1c9e-a47c-8141944f4190

What are the main differences between this rand function, and the one in the previous document?

What it the dot product operation doing? Why is the outcome so different to that in the first exercise? Consider how many outputs and inputs there are. Does this make a difference?

Alter the rand function to make sure it has frequency and amplitude arguments, similar to the first example. Now change these values and study their effects.

---

### The next few examples all use the random functions above in one way or another in order to modify the vertex buffer. When this happens, we need to update the normals, otherwise we can't light the shader properly. These exercises are designed to help you understand how to make sure you can do this properly. 


## Exercise 3

In the example below, we have shaded a geometry using a light, exactly as I describe in the lecture.

https://mimicproject.com/code/3ef97bc0-86b7-cced-40b7-3210a62a5475

Fork the document and make changes so that you can rotate the lighting.

Look at how the vertex shader is setting the value of the normal.

Make a note of all the steps required to pass this value to the Fragment shader.

Try to generate a random value and add it to the normal - what is another name for this process?

Now look at this document

https://mimicproject.com/code/8d036974-d345-ada9-b9bf-be4fc3b2eb21

What's going on? Can you rotate the sphere whilst retaining the lighting characteristics correctly?

---

## Exercise 4

https://mimicproject.com/code/4f968419-a78e-b4d4-bcc5-2722918b25ed

Notice that we are now using the perspective camera and a projection matrix (which is built in). These do the same things that we explored manually in Session 5.

The next step is to understand how to use matrix operations in the vertex shader. This exercise will help with that.

There are two main tasks :

a) Rescale the object using the scale matrix

b) Create a Rotation in a different axis - make sure your normals update

---

## Exercise 5

https://mimicproject.com/code/f1c2157e-b6d5-52d7-e0fa-b554826d03d2

This is a simple ground plane and it's not very good at all. The random number generator is being used to create terrain, but the terrain is not very varied or interesting. Your job is to make the terrain look better.

a) Create a translation so that the ground plane is on the ground - it's currently in the air!

b) Modify the terrain generator function (the random function) to make more interesting terrain. This is a bit like adding waves together over time + space... 

To help you with this, take a look at the below algorithms...

Fractal noise (value / Perlin noise)

https://mimicproject.com/code/01ca616c-3d47-ed3d-4082-18ecf7953ffe

Mandelbrot Shader

https://mimicproject.com/code/19644e9b-37e3-20de-6c9a-4bc3a5b47fd2

Consider how this affects the lighting - you might need to move the light. You might also need more lights. Can you do this?

Then, finally ....

c) Try to combine the ground plane with a second mesh object. If you can do this, congratulations you can more or less do anything...
