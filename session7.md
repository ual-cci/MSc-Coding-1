# Session 8: GLSL Shaders Part 1

# Introduction to GLSL using Fragment Shaders

* You now know how to build basic 3D worlds using GL.
* However, you may have also noticed that GL can be a little restrictive
* For example, dynamic systems are difficult to code.

# Part 1 : Review of Last Week's Session

- Last week we learned how to create more complex 3D scenes using Three.js. https://threejs.org/
- We also learned about how three.js is a library built on top of *webgl* https://get.webgl.org/
- We thought a little about how *3D models* are structured, and then used three.js to create Geometry.
- We learned about *Materials*, and that they are actually to do with the way light reflects of a 3D graphics object.
- We learned how to load and apply *Textures*, and considered how we 'map' textures to surfaces so that the pixel colours can be used to colour the surface of a mesh
- We thought about *Meshes* as combinations of *geometry* and *materials*, and that we need both of these things to create a mesh.
- We explore *light* objects by creating simple directional lighting in a 3D scene (without doing the maths by hand), and we thought about how different types of lights (Ambient, directional, specular) can be created in three.js
- We also introduced the notion of how *Triangles* are used to create surfaces from meshes - the cause of all the trouble!
- Finally, we thought hard about *Normals* - what they are, why you need them, how to create them and use them, and how they can be used to generate bump mapping

# HOMEWORK REVIEW

- I asked you to create a simple 3D scene using a small number of objects. 
- Hopefully this was achievable for everyone! If not, don't worry - try to work out what questions you have in your groups, and if you need specific help, remember, there are no bad questions when it comes to learning how to do creative computing.
- You may have noticed, as I mentioned earlier, that some things are easier to do using the 2D Projection method than when using three.js
- For example, dynamic geometry is hard!

- Break out in to your groups and review your work together :-)

---

# Part Two : Going Deeper, Doing it better

## Shaders

* To learn how to fully control webGL properly, you really need to learn how to use shaders.
* Shaders are absolutely nuts. They are easily the most exciting creative programming platform on the web, or perhaps anywhere.
* In my opinion, shader programming is one the best and most creative forms of programming, and one of the most exciting things you can do with a computer!
* No seriously, they are the about the most fun thing your computer can do.

## So what's so cool about shaders?

* What is amazing about shaders, is that they aren't just useful for graphics programming, they are used in all kinds of data processing, including the most advanced forms of AI and Machine Learning
* Tensorflow, Pytorch, and lots of other machine learning systems are heavily dependent on GPU hardware, and GPU hardware is programmed - you guessed it - using shaders :-)
* Learning to program shaders is a fantastic way to take full control of your computer, and the single most efficient method of computation
* They are also an excellent way to develop a better understanding of the mathematical basis of parallel computation, which is very very different to the way people traditionally learn to program.
* For example, remember the mandlebrot set we looked at a few weeks ago? That used two nested for loops to computer a test against every pixel value based on its position.
* To refresh your memory, here it is :

https://mimicproject.com/code/95b09168-00c1-b781-1cf1-9ba3761c276d

* Now, let's have a look at the shader version of this code

```JavaScript
precision mediump float;     
uniform float time;
uniform vec2 resolution;
uniform vec2 mouse;
            
void main()
{
vec2 c=(gl_FragCoord.xy-resolution/2.)/resolution.x*4.0*(-0.25*mouse.x) + (1.0-mouse.y);
float colour=0.;
vec2 z=vec2(0.);
for(int i=0;i<100;i++){
  colour++;
  if(dot(z,z) > 2.){break;}
  z=vec2(z.x*z.x-z.y*z.y,2.*z.x*z.y)+c;
}
gl_FragColor=vec4(vec3(colour/100.),1.);
}

```
- That's it.... it's less than 15 lines of code
- And it runs about 1000 times faster
- Let's have a look at another example

```JavaScript
precision mediump float;
uniform vec2 resolution;
uniform vec2 mouse;

void main(){
	vec3 p = vec3((gl_FragCoord.xy-resolution/2.0)/(resolution.y),mouse.x);

	for (int i = 0; i < 50; i++){
	   p = abs((abs(p)/dot(p, p)-1.0));
	   if(length(p) > 1.0 && length(p) < 1.01)break;
	}
	gl_FragColor.rgb = p;
	gl_FragColor.a = 1.0;
}
```

- What is apparent is that you can do much more complex things with far less code.
- Also, none of this code is writing in to an array - there's not a single array in sight (although there are some vectors).
- This is because we're not accessing a pixel buffer at all
- In the lecture, I'm going to take you through the magic of how this works
- But before I do, let's think about the creative communities that exist around GLSL :

## GLSL Communities

* Let's have a look at some links of the kinds of things that artists are doing with shaders
* There are two really important shader artists on the internet that the global shader community revolves around
* Ricardo Cabello - otherwise known as Mr Doob who you already know
* Inigo Quilez, otherwise known as...er... Inigo Quilez :-) https://iquilezles.org/

* They both have created online platforms with very active communities - *Shadertoy* (Quilez) and *glslsandbox* (Cabello).

- https://www.shadertoy.com - this is a really pleasant community with some incredible art on it
- http://glslsandbox.com - this place is not sanitised at all, and there is a great deal of trolling going on. However, there is also some amazing work, but **You may find some of the material offensive**. 

- Let's take a look at what these community platforms have to offer, and the kind of artworks you can find there. When we're looking at glslsandbox, remember that this is not our idea of a good community. 

## Getting started with GLSL
- Before we launch in to the lecture, let's look at a basic GLSL setup.
https://mimicproject.com/code/e2fb6d1d-e5f8-a950-5119-b47535a82752

You might also find this resource helpful
https://thebookofshaders.com/

# Part 3 : Lecture Part One

---

Grab the PDF presentation here:

- https://github.com/ual-cci/MSc-Coding-1/blob/master/Session-7-part1.pdf

---

## Homework 1

* Log in to mimicproject.com.

* Go to the following document and fork it:

https://mimicproject.com/code/62789edb-8cf2-e81b-4962-f129bb2268ab

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

# Lecture Part 2

Next, we need to look at the following presentation:

- https://github.com/ual-cci/MSc-Coding-1/blob/master/session7-part2.pdf

---

## Homework 2

Go to the following document and fork it:

https://mimicproject.com/code/86087fdf-04c8-61e1-f1b2-dc94711f968d

Here you can see a series of functions for creating squares and circles (Remember we're just working on the fragshader code)

You should notice that the square functions create squares, not rectangles.

1. Create a new function called "rectangle function" or similar that lets you specify the length of the sides of the rectangle independently.

If you are stuck, take a look at this:

https://mimicproject.com/code/1c83ae88-4117-38f8-216e-5a825f168314

Now try to create a simple picture with lots of rectangles, squares or circles of different colours. Remember you can add, subtract or multiply the outputs of functions. Make notes about the kinds of effects this can have.

2. Now, use a mat2 matrix to skew the sides of the square, or to rotate it. You can copy the rotation matrix from this code:

https://mimicproject.com/code/ef644559-9ad7-0e8a-b32b-2fbd7da69db1

Once you have done this, move on to part 3.

3. Fork this document:

https://mimicproject.com/code/0e84f212-142e-8cef-b427-fa1d8492f368

It shows you how to create lines.

* Do a complex line drawing using a sequence of lines that carry out specific functions.

Try to create expressions with combinations of sin, cos, tan, atan, pow etc. Look up the functions on shaderific for some inspiration.

* Experiment adding and subtracting the lines together. Remember that when you combine functions together, every pixel can be affected.

4. Extra credit:  Now fork this document.

https://mimicproject.com/code/8028d479-ec2f-e8ca-0bc8-891a4669d66f

This document has a vertex shader. Experiment with it to try to work out what it's doing. Can you create simple algorithmic geometry in this shader?

---
