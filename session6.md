# Session 6: 3D graphics part 2

* Making worlds

---

# So far..

* 3D geometry, vertices, unit vectors, directions, coordinate spaces, 2D perspective projection, matrices / transforms, openGL coordinates, primitives, procedural geometric forms.

---

# This week

* Intro to Three.js
* Geometry / Models
* Materials
* Textures
* Lighting
* Triangles
* Normals

---

# Programming techniques we will look at

* You should now be familiar with variables, conditionals, and loops.
* Today we will look more at scope
* We will look at functions in more detail
* We will also be using objects with specific methods defined by the Three.js API.
- https://threejs.org/docs/

---

# A word about Models

* In many cases, specifically where common forms of representation are being used (human characters for example), models are prepared outside of the rendering engine, then imported.
* In these cases, models are often groups of meshes, rather than one mesh. They may also have animations associated with them.
* In modern openGL, any element can be treated as an openGL NODE. Nodes can have parents, and children.
* Transforms affecting parents also affect children.
* You can have lots of children - e.g. lots of body parts.
* So you can think of models as groups of nodes organised in a hierarchy.

---

# A word about Models

* A model can also have all the features we are discussion today, baked in to the model for when you load it in the engine.
* These features include parameters that say how they will react to lighting such as materials,  normals), bump maps, and textures etc.
* They will also have specific information about how the model can be deformed.
* The entire package is a Resource.

---

# A word about Models

* We're going to be using basic geometry with Three.js
* But there's nothing stopping you from using models if you want.
* You can create, load, save and export models using Blender, which is a really fantastic piece of software:
- https://www.blender.org/

---

# Intro to Three.js

* Let's look at our basic Three.js example in detail.
* You can find it here:
- https://mimicproject.com/code/e252c3e4-ef71-774b-a9a0-870d8df20c0d
* Here we are going to look at lots of things:
* Basic Geometry, Materials, Meshes, Textures and Lighting.

---

# Intro to Three.js

* There are a group of objects in the scene that are standard and that you always need.
```javascript
var camera = new THREE.PerspectiveCamera(70, window.innerWidth / window.innerHeight, 1, 1000);
// We need to create a scene and add things to it.   
var scene = new THREE.Scene();
// Now we are goint to create some built in geometry 
// It's a box.    
var geometry = new THREE.BoxGeometry(200, 200, 200);
// We are going to want to texture the box.
// To do this we need a texture loader object to load the texture 
var myTextureLoader = new THREE.TextureLoader();
// Then we can load the texture into a variable
var myTexture = myTextureLoader.load('sgpic10.jpg');
// Now we need to create a material
// This defines how the surface of the object reflects light
// We're using Phong. There are lots of other types.      
var material = new THREE.MeshPhongMaterial({map: myTexture});
// We can now create a mesh using the geomentry and the material
var mesh = new THREE.Mesh(geometry, material);
// If we want to see stuff, we will need a light.
// The argument is the colour of the light in hexadecimal.      
var light = new THREE.DirectionalLight("rgb(255,255,255)");
// Now we can create our renderer. Thiis renders the scene. 
      
// There are lots of different kinds of renderers. 
// They also have a lot of parameters!!
var renderer = new THREE.WebGLRenderer({ preserveDrawingBuffer: true });
// We also create some camera controls. 
// These take the mouse info automatically and use it to control the scene.      
	var controls = new THREE.OrbitControls(camera, renderer.domElement); 
```
* The renderer here is slightly different to the one in the other example. What's the difference?
- Exercise - explore the introductory example and try to create a scene with more than one object. Animate the objects, and try to load different textures.

---

# Triangles

![triangles image](https://ual-cci.github.io/mick/images/1.jpg)

---

# Triangles

![triangles image](https://ual-cci.github.io/mick/images/2.jpg)

---

# Triangles

![triangles image](https://ual-cci.github.io/mick/images/3.jpg)

---

# Triangles

![triangles image](https://ual-cci.github.io/mick/images/4.jpg)

---

# Triangles

![triangles image](https://ual-cci.github.io/mick/images/5.jpg)

---

# Triangles

![triangles image](https://ual-cci.github.io/mick/images/6.jpg)

---

# Triangles

![triangles image](https://ual-cci.github.io/mick/images/7.jpg)

---

# Triangles

![triangles image](https://ual-cci.github.io/mick/images/8.jpg)

---

# Three.js dynamic geometry examples with triangle rendering
* You need to use this approach if you want to do dynamic geometry in three.js
- https://mimicproject.com/code/cbba9b28-522f-089b-25c0-a23cde718b6b
* This example is a little advanced, so don't worry if you don't get it straight away.

---

# Quads / Polygons

* You don’t need to use the triangle rendering method
* But it is the hardest one to get your head round.
* Quad Strip is very handy (more on this in a moment)
* Polygons are also great.
* Now you know how to organise points in a mesh to draw faces, you have a lot of skill.
* Most graphics programmers find this very hard :-)

---

# Lighting

* Three.js is based on WebGL, and can have lots of lights.
* OpenGL is limited to only 8, but you can create as many as you like using shaders :-)
* You can create and position various lights to illuminate a scene
* You can also adjust the ‘material’ properties of a 3D shape, to change how the object reacts to light

---

# Lighting

* These lights have various parameters, but basically they throw simulated light rays onto the scene.
* You can control how they do this very precisely

---

# Lighting

* There are 3 main lighting approaches in WebGL
* Ambient Light - the average emission from all sources in the scene
* Diffuse Light - directional light cast by a light source
* Specular Light - directional light that reflects off an object

---

# Lighting

* Ambient Light - this is flat shaded
* Diffuse Light - this makes it possible to create the illusion of depth when combined with ambient light
* Specular Light - this is the ‘shininess’ of the reflected light - can result in a highlight on an object, and infers something about  the material being used

---

# Lighting

* There is also emissive light - which is related to the colour of the object you are lighting
* In Three.js, there are lots of lighting options. Explore them!

---

# Vertex Normals

* A Normal is a vector perpendicular to the surface either from the surface centre, the vertex, or the object centre.
* Normals tell the renderer which direction the object or surface is facing.
* If the vertex Normal is pointing away from the viewer, you might not see the surface...

---

# Vertex Normals

* We can invert normals very easily in Three.js
* We do this be specifying which side is the surface
* We can do this when we set the material properties
* Material.side = THREE.BackSide, or Material.side = THREE.DoubleSide

---

# Vertex Normals

* When you have an object such as a sphere, with the origin in the centre, calculating the vertex normal is DEAD EASY
* The Vertex normal is the unit vector of the vertex position - the origin.
* This is because the unit vector of the vertex contains the direction that the vertex is going.
* The direction in these cases is perpendicular to the surface!!!

---

# Normals

![triangles image](https://ual-cci.github.io/mick/images/9.jpg)

---

# Normals

![triangles image](https://ual-cci.github.io/mick/images/10.jpg)

---

# Normals

![triangles image](https://ual-cci.github.io/mick/images/11.jpg)

---

# Bump Maps

* Bump maps are pretty great.
* They give the effect of altering the geometry by simply adjusting the direction of the normal.
* This makes the light reflect differently, just as if the geometry was a different shape.
* We'll look at these in more detail later.

---


# Textures

* Texture mapping is the most powerful method of creating coloured surfaces.
* It’s a bit complex, and there are a few rules to remember.

---

# Textures

* A texture needs to be uploaded to the graphics card
* Once there, you can bind it to the scene, draw with it, then unbind it.
* You can then bind a second texture in the same draw loop if you wish.
* This allows you to generate multi-textured scenes.

---


# Textures

* You can also load textures very easily and apply them to meshes
* You can see this in the earlier example.
---

# Environments

* When making 3D scenes, we use lights to generate more realistic looking environments
* In the example we’ve seen, there's an object lit with a texture.
* But we don’t have a sky.

---

# Environments

* The easiest method for generating a sky is to do the following:
* Create a cube
* Invert the normals so that they point inwards, not outwards (sometimes you don't need to do this)
* Make the cube very large, so that it fills the screen in all directions.
* texture map it with some sky.

---

# Environments

* This object is called a skybox
* They are super efficient, and you should use them

---

# TASK

* Build a 3D world with a surface, a sky, and some foreground objects
* You can use built in primitives.
* Don't forget to use textures.
* Use the example as a starting point.
