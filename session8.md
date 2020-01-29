# Session 8: GLSL Shaders Part 2

## Introduction to GLSL using Fragment Shaders

---
## GLSL shaders continued

Today we will be looking at noise generators for a little bit.

Then we will be looking at Vertex shaders in detail.

The main technical learning we are reinforcing are GLSL shader language operators (which are standard operators we have looked at before), and functions, because we need to use functions a lot in GLSL to simplify things.

If you are looking for the bump mapping example, you can find it here:

https://mimicproject.com/code/0d649cb7-0cca-a70a-86b2-f3e087402d12

---

## Presentation:

Grab the PDF presentation here:

- https://github.com/micknoise/Advanced-Creative-Coding-1/blob/master/Session-8.pdf

---

## Exercise 1

Log in to mimicproject.com.

Go to the following document and fork it:

https://mimicproject.com/code/b127c4fb-e76f-76e1-09ab-18973a61eedd

Locate the randfm function.

Find where the function is called. Alter the frequency and amplitude. What happens to the patterns at high amplitude?

Can you work out why this is happening?

---

## Exercise 2

Now go to this document and fork it:

https://mimicproject.com/code/15f43bb8-fecb-1c9e-a47c-8141944f4190

What are the main differences between this rand function, and the one in the previous document?

Try to figure out what the dot product is doing.

Alter the rand function so that it has frequency and amplitude arguments, like in the first example. Now change these values and study their effects.

---

## Exercise 3

https://mimicproject.com/code/3ef97bc0-86b7-cced-40b7-3210a62a5475

Set it up so that you can rotate the lighting.

Look at how the vertex shader is setting the normal.

Try to generate a random value and add it to the normal

Now look at this document

https://mimicproject.com/code/8d036974-d345-ada9-b9bf-be4fc3b2eb21

What's going on? Can you rotate the sphere whilst retaining the lighting characteristics correctly?

---

## Exercise 4

https://mimicproject.com/code/4f968419-a78e-b4d4-bcc5-2722918b25ed

Notice that we are now using the perspective camera.

a) Rescale the object using the scale matrix

b) Create a Rotation in a different axis - make sure your normals update

---

## Exercise 5

https://mimicproject.com/code/f1c2157e-b6d5-52d7-e0fa-b554826d03d2

Create a translation so that the ground plane is on the ground.

Consider how this affects the lighting - you might need to move the light..

---

## Exercise 6

Fractal noise (value / Perlin noise)

Try to apply one of the below fractal noise examples to the ground plane in 2)

https://mimicproject.com/code/01ca616c-3d47-ed3d-4082-18ecf7953ffe

Mandelbrot Shader

https://mimicproject.com/code/19644e9b-37e3-20de-6c9a-4bc3a5b47fd2

b) Try to combine the ground plane with a second mesh object. Use the earlier MIMIC document as a guide.
