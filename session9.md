# Session 9: Intro to Creative Machine Learning

## Introduction to fundamental machine learning concepts with RapidLib

---

## Presentation:

Grab the PDF presentation here:

- https://github.com/micknoise/Advanced-Creative-Coding-1/blob/master/Session-9.pdf

Start here:

* https://mimicproject.com/code/8de3cbbe-b7c6-d79f-65fa-42fd1aa43a26


## Exercise 1

In the first step, you'll be asked to include the rapidLib library

Substite that step for the below code:

<script src="https://www.doc.gold.ac.uk/eavi/rapidmix/RapidLib.js"></script>

Otherwise the tutorial should work.

Try entering inputs. Observe the outputs. Explore how the neural network produces results based on those inputs.

In particular:

* Try entering values that are higher than any of the values in the training set
* Try entering values that are lower than any of the values in the training set
* What do you notice about the Neural Network's behaviour?

You can grab the js code for the classification explorer here:

https://mimic-238710.appspot.com/asset/7addbbfe-b039-713d-f9b9-75a6cd00e923/classification-explorer.js



---

## Exercise 2

Take a look at the classification explorer here:

https://mimicproject.com/code/7f92bd4e-6d2b-181c-559f-4add766f2095

In order to input training examples, hold down a number key (e.g. 1) and move the mouse (you may have to click inside the example first to bring it into focus).

This will input examples of that class as long as you are holding down that number key. The decision boundary will then be displayed.

Try to choose a set of training examples that will draw the boundary with Class 1 on the left in green and Class 2 on the right in blue.

Try and make the line as straight as possible between the two classes.

Now try to make class 2 occupy the lower right quadrant.

* Have you had to manufacture examples close to the decision boundary to make it fit the shape?
* How might this effect the make-up of your datasets when working on an actual project?
* Will it just consist of representative examples of thing you are modelling?


---

## Exercise 3

Take a look at this example:

https://mimicproject.com/code/3864f3e5-8263-b70e-5ef9-1037c724d4ec

This extracts Mel-Frequency Ceptrum Coefficients and uses them as input to a KNN classifier.

Create a selection of classes and explore how good the system is.


---

## Exercise 4

Take a look at the Regression explorer:

https://mimicproject.com/code/26ab5507-0d25-07eb-cb03-aaa93883765d

* In order to input training examples, click onto screen at any point.

* The X value denotes the input value, whereas the y value denotes the output value. You will then see the regression line drawn as you add values.

* Try to get a feel for what types of lines are capable and how they’re influenced by the training data.

* Create a training set that produces a diagonal line from one corner of the canvas to the other.

* How easy is this to do? What issues do you face?

You can grab the js code for the regression explorer here.

https://mimic-238710.appspot.com/asset/26ab5507-0d25-07eb-cb03-aaa93883765d/regression-explorer.js

---

## Exercise 5

Now we are going to try and see if we can train a model with 3 outputs to behave consistently.

We’re going to one single input to control EXACTLY 3 output parameters.

Fork the below example:

https://mimicproject.com/code/5d67faaa-e4c3-771a-f824-fe5c5b978ab6

This is an example of using a slider as input to control a granular synthesiser (borrowed from Zya)

Granular synths play lots of small fragments (grains) of a soundfile at various positions.

* Play around with the two parameters and click on different parts of the waveform to find some sounds you like.

* When you are ready to record, select the "Record" checkbox.

* When you are ready to play, select the "Run" checkbox.

* This will train your model with the recorded dataset and now all 3 synthesiser parameters will be controlled by just the one value from the input slider.

* Keep recording examples until you can reliably control the output.

---

## Exercise 6

Can you take the simple RapdLib example we created at the start and use it to take different inputs, and control different outputs?

How about using the system for controlling a 3D mesh?

---

## Further reading

If you're interested in coding your own Neural Networks, this is a great tutorial :

https://karpathy.github.io/neuralnets/
