# Gradient_descent_Complete_In_Depth_for beginners
## 0.1 Table of Contents<a class="anchor" id="0.1"></a>
1. [Let's talk about Differential Derivative and Partial Derivative](#1)
    - 1.1 [What is Differential?](#1.1)
    - 1.2 [What is Derivative?](#1.2)
    - 1.3 [Partial Derivation (Differentiation)](#1.3)
2. [Gradient Descent](#2)
    - 2.1 [What is Gradient Descent?](#2.1)
    - 2.2 [The Cost function](#2.2)
    - 2.3 [All Loss Functions](#2.3)
    - - 2.3 A) [The Difference between Loss and Cost Function](#2.3A)
    - 2.4 [Linear Regression using Gradient Descent](#2.4)
    - 2.5 [Initialization](#2.5)
    - 2.6 [Direction and learning Rate](#2.6)
    - 2.7 [Challenges with Gradient Descent](#2.7)
    - 2.8 [Types of Gradient Descent](#2.8)
    - 2.9 [Variants of Gradient Descent Algorithm](#2.9)
3. [Overview](#3)

## 1. Let's talk about Differential Derivative and Partial Derivative<a class="anchor" id="1"></a>
+ To better understand the difference between the differential and derivative of a function. You need to understand the concept of a function.
  
+ A function is one of the basic concepts in mathematics that defines a relationship between a set of inputs and a set of possible outputs where each input is related to one output. Where Input variables are the independent variables and the other which is output variable is the dependent variable.
  
+ Take for example the statement " 'y' is a function of $x$ i.e y= $f(x)$ which means something related to y is directly related to x by some formula.
  
+ The Calculus as a tool defines the derivative of a function as the limit of a particular kind.
#### 1.1 What is Differential?<a class="anchor" id="1.1"></a>
___
It is one of the fundamentals divisions of calculus, along with integral calculus. It is a subfield of calculus that deals with infinitesimal change in some varying quantity. The world we live in is full of interrelated quantities that change periodically.

For example, the area of a circular body which changes as the radius changes or a projectile which changes with the velocity. These changing entities, in mathematical terms, are called as variables and **the rate of change of one variable with respect to another is a `derivative`**. **And the equation which represents the relationship between these variables is called a `differential equation.`**
#### 1.2 What is Derivative?<a class="anchor" id="1.2"></a>
  The derivative of a function represents an instantaneous rate of change in the value of a dependent variable with respect to the change in value of the independent variable. **`It’s a fundamental tool of calculus which can also be interpreted as the slope of the tangent line.`** It measures how steep the graph of a function is at some given point on the graph.
  
+ It measures how steep the graph of a function is at some given point on the graph
    
+ Equations which define relationship between there variables and their derivatives are called Differential Equations.
    
+ Differentiation is the process of finding a derivative.
    
+ The derivative of a function is the rate of change of the output value with respect to its input value, where as differential is the actual change of function.
    
+ Differentials are represented as $d_x$, $d_y$, $d_t$, and so on, where $d_x$ represents a small change in $x$, etc.
    
+ When comparing changes in related quantities where y is the function of x, the differential $d_y$ is written as y = $f$(x)
+ $\frac{d_y}{d_x}=f(x)$
+ The derivative of a function is the slope of the function at any point and is written as $\frac{d}{d_x}$.
+ For example, the derivative of $sin(x)$ can be written as $\frac{d_{sin(x)}}{d_x}=cos(x)$
### 1.3 Partial Derivation (Differentiation)<a class="anchor" id="1.3"></a>
___

Partial differentiation is used to differentiate mathematical functions having more than one variable in them. In ordinary differentiation, we find derivative with respect to one variable only, as function contains only one variable. So partial differentiation is more general than ordinary differentiation. **`Partial differentiation is used for finding maxima and minima in optimization problems`**.

It is a derivative where we hold some independent variable as constant and find derivative with respect to another independent variable.

For example, suppose we have an equation of a curve with X and Y coordinates in it as 2 independent variables. To find the slope in the direction of X, while keeping Y fixed, we will find the partial derivative. Similarly, we can find the slope in the direction of Y (keeping X as Fixed).

Example: consider $f$ = 4$x^2$ + 3y + z 
The partial derivative of the above equation with respect to x is $f^{'}$ = 8$x$

In ordinary differentition the same equation goes like $f_{'}$ = 8$x$ + 3$\frac{d_y}{d_x}$ + $\frac{d_z}{d_x}$

![image](https://user-images.githubusercontent.com/99672298/181267289-b7699632-b5ec-41db-9419-473e2075f248.png)

[Table of Content](#0.1)
## 2. Gradient Descent<a class="anchor" id="2"></a>

![01 07 2022_23 33 59_REC](https://user-images.githubusercontent.com/99672298/181736933-b8257ea0-c86a-4a7e-b188-b0b09c031643.png)

+ Optimization is the core of every machine learning algorithm

### 2.1 What is Gradient Descent?<a class="anchor" id="2.1"></a>
___

To explain Gradient Descent I’ll use the classic mountaineering example.

Suppose you are at the top of a mountain, and you have to reach a lake which is at the lowest point of the mountain (a.k.a valley). A twist is that you are blindfolded and you have zero visibility to see where you are headed. So, what approach will you take to reach the lake?

The best way is to check the ground near you and observe where the land tends to descend. This will give an idea in what direction you should take your first step. If you follow the descending path, it is very likely you would reach the lake.

To represent this graphically, notice the below graph.

![image](https://user-images.githubusercontent.com/99672298/181270129-ad968808-f5d8-4e1c-9f43-87ecbe73ef1c.png)

Let us now map this scenario in mathematical terms.

Suppose we want to find out the best parameters (θ1) and (θ2) for our learning algorithm. Similar to the analogy above, we see we find similar mountains and valleys when we plot our “cost space”. Cost space is nothing but how our algorithm would perform when we choose a particular value for a parameter.

So on the y-axis, we have the cost J(θ) against our parameters θ1 and θ2 on x-axis and z-axis respectively. Here, hills are represented by red region, which have high cost, and valleys are represented by blue region, which have low cost.

![image](https://user-images.githubusercontent.com/99672298/181286388-e82f5cec-6c54-442a-af27-6a84d49ed69e.png)
![28 06 2022_11 06 50_REC](https://user-images.githubusercontent.com/99672298/181739571-fd6c011a-ec82-4b3f-979d-0ec7d0382d42.png)

### 2.2 The Cost function<a class="anchor" id="2.2"></a>
___
It is defind as the measurement of difference of error between actual values and expected values at the current position

The slight difference between the loss fucntion and the cost function is about the error within the training of machine learning models, as loss function refers to the errors of one training example, while a cost function calculates the average error across on entire training set.

+ Gradient descent is an optimization algorithm that works iteratively to find the model parameters with minimal cost or error values. If we go through a formal definition of Gradient descent

+ Gradient descent is a first-order iterative optimization algorithm for finding a local minimum of a differentiable function.Gradient descent is an optimization algorithm used to optimize neural networks and many other machine learning algorithms. Our main goal in optimization is to find the local minima, and gradient descent helps us to take repeated steps in the direction opposite of the gradient of the function at the current point. This method is commonly used in machine learning (ML) and deep learning (DL) to minimize a cost/loss function

### 2.3 All Loss functions<a class="anchor" id="2.3"></a>
___
+ **`Mean Squared Error`**
+ The Mean Squared Error (MSE) is perhaps the simplest and most common loss function, often taught in introductory Machine Learning courses. To calculate the MSE, you take the difference between your model’s predictions and the ground truth, square it, and average it out across the whole dataset.

The MSE will never be negative, since we are always squaring the errors. The MSE is formally defined by the following equation:

![image](https://user-images.githubusercontent.com/99672298/186230924-9597c187-b6ea-42b0-9071-e0ee2fbf38a4.png)

Where N is the number of samples we are testing against.

![image](https://user-images.githubusercontent.com/99672298/186230986-1a796c76-15f4-4bc9-a4d8-487ae0bfa425.png)

![17 08 2022_19 31 44_REC](https://user-images.githubusercontent.com/99672298/186230025-9aa1e21c-e2b3-466a-ad6d-b4e27f68cb35.png)

![17 08 2022_19 27 56_REC](https://user-images.githubusercontent.com/99672298/186229944-393a5f83-f42b-43de-9617-9d81ca4d2857.png)

Advantage: The MSE is great for ensuring that our trained model has no outlier predictions with huge errors, since the MSE puts larger weight on theses errors due to the squaring part of the function.

Disadvantage: If our model makes a single very bad prediction, the squaring part of the function magnifies the error. Yet in many practical cases we don’t care much about these outliers and are aiming for more of a well-rounded model that performs good enough on the majority.

+ **`Absolute Error loss`**

The Mean Absolute Error (MAE) is only slightly different in definition from the MSE, but interestingly provides almost exactly opposite properties! To calculate the MAE, you take the difference between your model’s predictions and the ground truth, apply the absolute value to that difference, and then average it out across the whole dataset.

The MAE, like the MSE, will never be negative since in this case we are always taking the absolute value of the errors. The MAE is formally defined by the following equation:

![image](https://user-images.githubusercontent.com/99672298/186231183-38e3ce23-81c0-4aa1-9288-293cfdf7fada.png)
![image](https://user-images.githubusercontent.com/99672298/186231224-60e02b0c-5d6b-4a96-8060-7a4bca963c9b.png)
![17 08 2022_20 09 47_REC](https://user-images.githubusercontent.com/99672298/186230150-93a80714-bb2f-47bb-899a-b497c49fda2c.png)
![17 08 2022_21 43 06_REC](https://user-images.githubusercontent.com/99672298/186230261-51f220ff-b1a6-4bcc-a453-08d1a9b0ee71.png)

Advantage: The beauty of the MAE is that its advantage directly covers the MSE disadvantage. Since we are taking the absolute value, all of the errors will be weighted on the same linear scale. Thus, unlike the MSE, we won’t be putting too much weight on our outliers and our loss function provides a generic and even measure of how well our model is performing.

Disadvantage: If we do in fact care about the outlier predictions of our model, then the MAE won’t be as effective. The large errors coming from the outliers end up being weighted the exact same as lower errors. This might results in our model being great most of the time, but making a few very poor predictions every so-often.

+ **`Huber Loss`**

Now we know that the MSE is great for learning outliers while the MAE is great for ignoring them. But what about something in the middle?

Consider an example where we have a dataset of 100 values we would like our model to be trained to predict. Out of all that data, 25% of the expected values are 5 while the other 75% are 10.

An MSE loss wouldn’t quite do the trick, since we don’t really have “outliers”; 25% is by no means a small fraction. On the other hand we don’t necessarily want to weight that 25% too low with an MAE. Those values of 5 aren’t close to the median (10 — since 75% of the points have a value of 10), but they’re also not really outliers.

Our solution?

The Huber Loss Function.

The Huber Loss offers the best of both worlds by balancing the MSE and MAE together. We can define it using the following piecewise function:

![image](https://user-images.githubusercontent.com/99672298/186231537-ee7e5aa3-377a-4e9a-8e8e-241a21b4f9d7.png)

**`What this equation essentially says is: for loss values less than delta, use the MSE; for loss values greater than delta, use the MAE.`** This effectively combines the best of both worlds from the two loss functions!

Using the MAE for larger loss values mitigates the weight that we put on outliers so that we still get a well-rounded model. At the same time we use the MSE for the smaller loss values to maintain a quadratic function near the centre.

This has the effect of magnifying the loss values as long as they are greater than 1. Once the loss for those data points dips below 1, the quadratic function down-weights them to focus the training on the higher-error data points.

![17 08 2022_21 42 39_REC](https://user-images.githubusercontent.com/99672298/186230181-f7267037-7561-48c6-83f6-4234c9da9470.png)

+ **`Cross Entropy`**

![17 08 2022_21 51 22_REC](https://user-images.githubusercontent.com/99672298/186230361-09ceb50b-7032-4af3-9338-bd51e98f27e4.png)

If you are training a binary classifier, chances are you are using binary cross-entropy / log loss as your loss function.

A Simple Classification Problem
Let’s start with 10 random points:

x = [-2.2, -1.4, -0.8, 0.2, 0.4, 0.8, 1.2, 2.2, 2.9, 4.6]

This is our only feature: x.

![image](https://user-images.githubusercontent.com/99672298/186340993-dc40bded-8290-454b-aa10-d3e9d398b2ab.png)

Now, let’s assign some colors to our points: red and green. These are our labels

![image](https://user-images.githubusercontent.com/99672298/186341040-92621a17-6b98-4be8-9be4-23c2a2b5558a.png)

So, our classification problem is quite straightforward: given our feature x, we need to predict its label: red or green.

Since this is a binary classification, we can also pose this problem as: “is the point green” or, even better, “what is the probability of the point being green”? Ideally, green points would have a probability of 1.0 (of being green), while red points would have a probability of 0.0 (of being green).

In this setting, green points belong to the positive class (YES, they are green), while red points belong to the negative class (NO, they are not green).

If we fit a model to perform this classification, it will predict a probability of being green to each one of our points. Given what we know about the color of the points, how can we evaluate how good (or bad) are the predicted probabilities? This is the whole purpose of the loss function! It should return high values for bad predictions and low values for good predictions.

For a binary classification like our example, the typical loss function is the binary cross-entropy / log loss.

+ **Loss Function: Binary Cross-Entropy / Log Loss**

If you look this loss function up, this is what you’ll find:

![image](https://user-images.githubusercontent.com/99672298/186341521-0fe42e12-7309-4f8c-88af-c70b26a46bef.png)

where y is the label (1 for green points and 0 for red points) and p(y) is the predicted probability of the point being green for all N points.

Reading this formula, it tells you that, for each green point (y=1), it adds log(p(y)) to the loss, that is, the log probability of it being green. Conversely, it adds log(1-p(y)), that is, the log probability of it being red, for each red point (y=0). Not necessarily difficult, sure, but no so intuitive too…

But, before going into more formulas, let me show you a visual representation of the formula above…

Computing the Loss — the visual way
First, let’s split the points according to their classes, positive or negative, like the figure below:

![image](https://user-images.githubusercontent.com/99672298/186342684-4b990292-e652-482d-aaff-bb8e6b220310.png)

Now, let’s train a Logistic Regression to classify our points. The fitted regression is a sigmoid curve representing the probability of a point being green for any given x . It looks like this:

![image](https://user-images.githubusercontent.com/99672298/186342708-920ac9a1-1969-4bc2-a97b-22ed8db5e34d.png)

Then, for all points belonging to the positive class (green), what are the predicted probabilities given by our classifier? These are the green bars under the sigmoid curve, at the x coordinates corresponding to the points.

![image](https://user-images.githubusercontent.com/99672298/186342733-4995cec9-0903-4c21-8225-232f3262917d.png)

OK, so far, so good! What about the points in the negative class? Remember, the green bars under the sigmoid curve represent the probability of a given point being green. So, what is the probability of a given point being red? The red bars ABOVE the sigmoid curve, of course :-)

![image](https://user-images.githubusercontent.com/99672298/186342774-f55afca5-e094-4fa3-bbc4-fa43d85cdbb7.png)

Putting it all together, we end up with something like this:

![image](https://user-images.githubusercontent.com/99672298/186342812-c5549022-ae7c-40b0-9fe0-d4561e4f0b49.png)

The bars represent the predicted probabilities associated with the corresponding true class of each point!

OK, we have the predicted probabilities… time to evaluate them by computing the binary cross-entropy / log loss!

These probabilities are all we need, so, let’s get rid of the x axis and bring the bars next to each other:

![image](https://user-images.githubusercontent.com/99672298/186342852-053bb37a-602e-4b85-a9c7-a1c4360f46a6.png)

Well, the hanging bars don’t make much sense anymore, so let’s reposition them:

![image](https://user-images.githubusercontent.com/99672298/186342909-c51d7c4a-1720-4720-9822-775caafd5826.png)

Since we’re trying to compute a loss, we need to penalize bad predictions, right? If the probability associated with the true class is 1.0, we need its loss to be zero. Conversely, if that probability is low, say, 0.01, we need its loss to be HUGE!

It turns out, taking the (negative) log of the probability suits us well enough for this purpose (since the log of values between 0.0 and 1.0 is negative, we take the negative log to obtain a positive value for the loss).

The plot below gives us a clear picture —as the predicted probability of the true class gets closer to zero, the loss increases exponentially:

![image](https://user-images.githubusercontent.com/99672298/186342975-83dc301a-1cee-4620-9795-69cebc36179d.png)

Fair enough! Let’s take the (negative) log of the probabilities — these are the corresponding losses of each and every point.

Finally, we compute the mean of all these losses.

![image](https://user-images.githubusercontent.com/99672298/186342998-4f783796-0fba-4531-baca-67c1b0b78108.png)

Voilà! We have successfully computed the binary cross-entropy / log loss of this toy example. It is 0.3329!

+ **Distribution**

Let’s start with the distribution of our points. Since y represents the classes of our points (we have 3 red points and 7 green points), this is what its distribution, let’s call it q(y), looks like:

![image](https://user-images.githubusercontent.com/99672298/186344163-15e8c7db-c40a-42b0-b869-1916096e531e.png)

+ **Entropy**

`Entropy is a measure of the uncertainty associated with a given distribution q(y).`

What if all our points were green? What would be the uncertainty of that distribution? ZERO, right? After all, there would be no doubt about the color of a point: it is always green! So, entropy is zero!

On the other hand, what if we knew exactly half of the points were green and the other half, red? That’s the worst case scenario, right? We would have absolutely no edge on guessing the color of a point: it is totally random! For that case, entropy is given by the formula below (we have two classes (colors)— red or green — hence, 

![image](https://user-images.githubusercontent.com/99672298/186344236-f42698c6-c8ac-4618-8fe0-56e3f43fa922.png)

For every other case in between, we can compute the entropy of a distribution, like our q(y), using the formula below, where C is the number of classes:

![image](https://user-images.githubusercontent.com/99672298/186344265-28164ce4-2a3d-4a76-b420-886e2d347339.png)

So, if we know the true distribution of a random variable, we can compute its entropy. But, if that’s the case, why bother training a classifier in the first place? After all, we KNOW the true distribution…

But, what if we DON’T? Can we try to approximate the true distribution with some other distribution, say, p(y)? Sure we can! :-)

+ **Cross-Entropy**

Let’s assume our points follow this other distribution p(y). But we know they are actually coming from the true (unknown) distribution q(y), right?

If we compute entropy like this, we are actually computing the cross-entropy between both distributions:

![image](https://user-images.githubusercontent.com/99672298/186344308-da1764b0-dc2a-4bfe-a5e7-a05fe22d33bc.png)

If we, somewhat miraculously, match p(y) to q(y) perfectly, the computed values for both cross-entropy and entropy will match as well.

Since this is likely never happening, cross-entropy will have a BIGGER value than the entropy computed on the true distribution.

![image](https://user-images.githubusercontent.com/99672298/186344349-88f7a7f9-3d40-48b8-9ccb-ab299259d0af.png)

It turns out, this difference between cross-entropy and entropy has a name…

+ **Kullback-Leibler Divergence**

The Kullback-Leibler Divergence,or “KL Divergence” for short, is a measure of dissimilarity between two distributions:

![image](https://user-images.githubusercontent.com/99672298/186344413-2ffb75ec-fa5a-405d-a129-268074671d98.png)

This means that, the closer p(y) gets to q(y), the lower the divergence and, consequently, the cross-entropy, will be.

So, we need to find a good p(y) to use… but, this is what our classifier should do, isn’t it?! And indeed it does! It looks for the best possible p(y), which is the one that minimizes the cross-entropy.

+ **Loss Function** 

During its training, the classifier uses each of the N points in its training set to compute the cross-entropy loss, effectively fitting the distribution p(y)! Since the probability of each point is 1/N, cross-entropy is given by:

![image](https://user-images.githubusercontent.com/99672298/186344500-67759c7a-a289-48da-bacf-7934ad8710e3.png)

Remember Figures 6 to 10 above? We need to compute the cross-entropy on top of the probabilities associated with the true class of each point. It means using the green bars for the points in the positive class (y=1) and the red hanging bars for the points in the negative class (y=0) or, mathematically speaking:

![image](https://user-images.githubusercontent.com/99672298/186344528-30098ee8-df79-46ad-8afd-d037ec25d1a5.png)

The final step is to compute the average of all points in both classes, positive and negative:

![image](https://user-images.githubusercontent.com/99672298/186344578-59c3aed2-d99a-4725-9d45-dcd64069fef3.png)

Finally, with a little bit of manipulation, we can take any point, either from the positive or negative classes, under the same formula:

![image](https://user-images.githubusercontent.com/99672298/186344607-f2ced279-d912-4e35-a2a9-3a85778f9ea3.png)

Voilà! We got back to the original formula for binary cross-entropy / log loss :-)

Binary Cross Entropy for Multi-Class classification
If you are dealing with a multi-class classification problem you can calculate the Log loss in the same way. Just use the formula given below.

![image](https://user-images.githubusercontent.com/99672298/186344912-feabc467-d5ad-47de-9900-26223b30d661.png)

+ **`Multi-Class Cross Entropy`**

![17 08 2022_21 57 18_REC](https://user-images.githubusercontent.com/99672298/186230519-5af07bb8-34f5-4fa7-96d5-ee1b06f10010.png)
![18 08 2022_10 52 46_REC](https://user-images.githubusercontent.com/99672298/186230575-85ec562c-fb9d-4ad7-9197-567d6725c39f.png)

+ **Categorical crossentropy**
Categorical crossentropy is a loss function that is used in multi-class classification tasks. These are tasks where an example can only belong to one out of many possible categories, and the model must decide which one.
Formally, it is designed to quantify the difference between two probability distributions.

![image](https://user-images.githubusercontent.com/99672298/186352375-108d18e5-f56f-40e6-9a0b-60055f56338a.png)

Categorical crossentropy math
The categorical crossentropy loss function calculates the loss of an example by computing the following sum:

![image](https://user-images.githubusercontent.com/99672298/186351930-f71cfbf5-b14c-4ef5-92d1-7fd03703043e.png)

Sigmoid
It squashes a vector in the range (0, 1). It is applied independently to each element of $s$ $s_i$. It’s also called **logistic function.**

![image](https://user-images.githubusercontent.com/99672298/186352719-e67d98a6-c6e7-4ef1-a055-ab1ab3471142.png)
![image](https://user-images.githubusercontent.com/99672298/186352760-e5bc95a9-f8ed-4155-9edf-c57296b911f3.png)

Softmax
Softmax it’s a function, not a loss. It squashes a vector in the range (0, 1) and all the resulting elements add up to 1. It is applied to the output scores $s$. As elements represent a class, they can be interpreted as class probabilities.
The Softmax function cannot be applied independently to each $s_i$, since it depends on all elements of $s$. For a given class $s_i$, the Softmax function can be computed as:

![image](https://user-images.githubusercontent.com/99672298/186352988-8f64c8c9-df08-4cf5-811c-ce8000cd1175.png)


![18 08 2022_11 18 57_REC](https://user-images.githubusercontent.com/99672298/186230590-6a9f100b-41c1-47ac-a1df-a27e551226fe.png)
![18 08 2022_11 20 51_REC](https://user-images.githubusercontent.com/99672298/186230630-14021cdd-f7ff-4a72-8de4-dc020a9ff350.png)

#### 2.3 A) The difference between the Loss Function and the Cost Function<a class="anchor" id="2.3A"></a>

Loss function vs Cost function
Most people confuse loss function and cost function. let’s understand what is loss function and cost function. Cost function and Loss function are synonymous and used interchangeably but they are different.

Loss Function:

A loss function/error function is for a single training example/input.

Cost Function:

A cost function, on the other hand, is the average loss over the entire training dataset.

![17 08 2022_15 54 58_REC](https://user-images.githubusercontent.com/99672298/186229903-293fe2e5-34c4-430a-b24a-5ba8bc63f3c2.png)

#### Loss Functions
The loss function quantifies how much a model \boldsymbol{f}‘s prediction \boldsymbol{\hat{y} \equiv f(\mathbf{x})} deviates from the ground truth \boldsymbol{y \equiv y(\mathbf{x})} for one particular object \mathbf{x}. So, when we calculate loss, we do it for a single object in the training or test sets.

There are many different loss functions we can choose from, and each has its advantages and shortcomings. In general, any distance metric defined over the space of target values can act as a loss function.

Example: the Square and Absolute Losses in Regression
Very often, we use the square(d) error as the loss function in regression problems:

![Filter_Method](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-55cdb152abd779c1153eba17ff703543_l3.svg)

For instance, let’s say that our model predicts a flat’s price (in thousands of dollars) based on the number of rooms, area (m^2), floor, and the neighborhood in the city (A or B). Let’s suppose that its prediction for \mathbf{x} = \begin{bmatrix} 4, 70, 1, A \end{bmatrix} is USD 110k. If the actual selling price is USD 105k, then the square loss is:

![Filter_Method](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-c3c793b54c64edf52d286a303fd1dc6c_l3.svg)

Another loss function we often use for regression is the absolute loss:

![Filter_Method](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-84c87f085f9982b6bc21afd953ec995a_l3.svg)

In our example with apartment prices, its value will be:

![Filter_Method](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-d9d8f4b2520f21bf8a7416387fbba268_l3.svg)

Choosing the loss function isn’t an easy task. Through cost, loss plays a critical role in fitting a model.

#### Cost Functions
The term cost is often used as synonymous with loss. However, some authors make a clear difference between the two. For them, the cost function measures the model’s error on a group of objects, whereas the loss function deals with a single data instance.

So, if L is our loss function, then we calculate the cost function by aggregating the loss L over the training, validation, or test data \mathcal{D}= \left\{ (\mathbf{x}_i, y_i) \right\}_{i=1}^{n}. For example, we can compute the cost as the mean loss:

![Filter_Method](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-a1db1deca69cb960993357d35c5d47cf_l3.svg)

But, nothing stops us from using the median, the summary statistic less sensitive to outliers:

![Filter_Method](https://www.baeldung.com/wp-content/ql-cache/quicklatex.com-bc20907c9597f07aa054f74770e3ae93_l3.svg)

The cost functions serve two purposes. First, its value for the test data estimates our model’s performance on unseen objects. That allows us to compare different models and choose the best. Second, we use it to train our models.

![Filter_Method](https://editor.analyticsvidhya.com/uploads/25665ezgif.com-gif-maker.gif)

### 2.4 Linear Regression using Gradient Descent<a class="anchor" id="2.4"></a>
___

![Filter Method](https://miro.medium.com/max/1400/1*CjTBNFUEI_IokEOXJ00zKw.gif)

A straight line is represented by using the formula y = m$x$ + c
+ y is the dependent variable
+ $x$ is independent variable
+ m is the slope of the line
+ c is the y intercept

![image](https://user-images.githubusercontent.com/99672298/181279168-8949b883-3cb1-4a6f-a7d6-70a506a67ff8.png)
![28 06 2022_11 15 26_REC](https://user-images.githubusercontent.com/99672298/181739676-ab46314b-e12f-4596-b8ad-01ee6bcacdb6.png)

#### (MSE) Loss Function
___

We will use the Mean Squared Error function to calculate the loss. There are three steps in this function:

+ Find the difference between the actual y and predicted y value(y = mx + c), for a given x.
+ Square this difference.
+ Find the mean of the squares for every value in X.

![image](https://user-images.githubusercontent.com/99672298/181279524-875c3382-4732-42f8-bf25-699bb33a5e91.png)

Here yᵢ is the actual value and ȳᵢ is the predicted value. Lets substitute the value of ȳᵢ:

![image](https://user-images.githubusercontent.com/99672298/181279573-e5b8c097-87c3-4527-b249-98cb45d30dd6.png)

**The loss function helps to increase and improve machine learning efficiency by providing feedback to the model, so that it can minimize error and find the global minima. Further, it continuously iterates along the direction of the negative gradient until the cost function approaches zero.**

Calculating the partial derivative of the cost function with respect to slope (m), let the partial derivative of the cost function with respect to m be $D_m$

Let’s try applying gradient descent to m and c and approach it step by step:

+ Initially let m = 0 and c = 0. Let L be our learning rate. This controls how much the value of m changes with each step. L could be a small value like 0.0001 for good accuracy.
+ Calculate the partial derivative of the loss function with respect to m, and plug in the current values of x, y, m and c in it to obtain the derivative value D.

![image](https://user-images.githubusercontent.com/99672298/181281437-486385c4-62fe-40c5-9e31-5fbd754f72d9.png)

Dₘ is the value of the partial derivative with respect to m. Similarly lets find the partial derivative with respect to c, Dc :

![image](https://user-images.githubusercontent.com/99672298/181281479-5faf1ffd-cb17-42c0-afd7-9a755a1cef02.png)

+ Now we update the current value of m and c using the following equation:

![image](https://user-images.githubusercontent.com/99672298/181281560-2742cbd0-cc4c-4d80-966f-3697d230ed79.png)

+ We repeat this process until our loss function is a very small value or ideally 0 (which means 0 error or 100% accuracy). The value of m and c that we are left with now will be the optimum values.

[Table of Content](#0.1)

### 2.5 Initialization<a class="anchor" id="2.5"></a>
___
 The Starting point is a randomly selected value of slope and intercept (m & c). It is used as a starting point, to derive the first derivative or slope and then uses the tangent line to calculate the steepness of the slope. Further, this slope will inform the update to the parameters. The slope becomees steeper at eht starting point, but whenever new paramters are generated, then the steepness gradually reduces, the closer we get to the optimal value, the closer the slope of the curve gets to zero. This means that wehtn the slope of the cruve is close to zero, which is claled as that we are near to the point of convergence.

![02 07 2022_11 29 16_REC](https://user-images.githubusercontent.com/99672298/181737076-62bdea0e-c817-4f1d-abbb-823adc48b56e.png)
![28 06 2022_15 21 14_REC](https://user-images.githubusercontent.com/99672298/181740063-af623d4e-ac3e-4ece-a460-e6db9e906899.png)

### 2.6 Direction and learning Rate<a class="anchor" id="2.6"></a>
___

These two factors are used to determine the partial derivative calculation of future iteration and allow it to the point of convergence or glabal minima.

#### Learning Rate 
___

It is defined as the step size taken to reach the minima or lowest point. It has a strong influence on performance. It controls how much the value of m (slope) and c (intercept) changes withe each step.
 
Let "L" be the learning rate
 
+ step_size = $D_c$ x L
+ step_size = $D_m$ x learning_rate(L)
+ New_slope = old_slope - stepsize
+ New_intercept = old_intercept - stepsize
 
+ **Smaller learning rate:** the model will take too much time before it reaches minima might even exhaust the max iterations specified.

![](https://editor.analyticsvidhya.com/uploads/26393ezgif.com-gif-maker%20(5).gif)
+ **Large (Big learning rate):** the steps taken will be large and we can even miss the minima the algorithm may not converge to the optimal point.
+ Because the steps size being too big, it simply jumping back and forth between the convex function of gradient descent. In our case even if we continue till ith iteration we will not reach the local minima.

![f](https://editor.analyticsvidhya.com/uploads/81207ezgif.com-gif-maker%20(4).gif)

+ **The learning rate should be an optimum value.**
+ If the learning rate is high, it results in larger steps but also leads to risk of overshooting the minimum. At the same time, a low (small) learning rate shows the small step size, which compromises overall efficeincy but gives the advantage of more precision.

![f](https://editor.analyticsvidhya.com/uploads/94236ezgif.com-gif-maker%20(7).gif)
![image](https://user-images.githubusercontent.com/99672298/181450732-7108af01-d47c-4688-9438-38948430f16c.png)

#### In summary, Gradient Descent methods steps are
___

1.) Choose starting point (initialisation).\
2.) Calculate gradient at that point.\
3.) Make a scaled step in the opposite direction to the gradient
#### The closer we get to the optimal value the closer the slope of the curve gets to 0 and when this happens which means we should take small steps, because we are close to the optimal value and when the case is opposite of this we should take big steps.
4.) We repeat this process until our loss function is a very small value. The value of m and c that we are left with now will be the optimum values.

![12 05 2022_16 18 16_REC](https://user-images.githubusercontent.com/99672298/181741402-f87b9ed0-dc55-4f0e-8eba-e721000dcdd5.png)
![29 06 2022_11 49 50_REC](https://user-images.githubusercontent.com/99672298/181743311-a7211485-a49e-46b6-ba79-e47be229809a.png)
![12 05 2022_16 17 32_REC](https://user-images.githubusercontent.com/99672298/181741930-cf91b410-eff4-4f20-8c0a-7c7e3e4b4289.png)
![29 06 2022_11 50 05_REC](https://user-images.githubusercontent.com/99672298/181744015-b42eff82-5aaf-4e23-8dc7-c89fc4afe6bd.png)
![29 06 2022_11 50 21_REC](https://user-images.githubusercontent.com/99672298/181744168-33a9f243-7de1-4c99-836d-a845b9a98ec7.png)
![29 06 2022_11 49 33_REC](https://user-images.githubusercontent.com/99672298/181742233-8438053b-3b95-4d83-86a5-284dab348a55.png)
![29 06 2022_11 51 02_REC](https://user-images.githubusercontent.com/99672298/181744370-362df2ee-ca9a-4223-9b9c-e025a91d76c1.png)
![12 05 2022_19 10 11_REC](https://user-images.githubusercontent.com/99672298/181742542-f6e91382-8088-4f40-86c1-98773f9e2117.png)
![29 06 2022_11 54 26_REC](https://user-images.githubusercontent.com/99672298/181744604-a04be59a-4889-4619-b09b-28d25f218757.png)
![29 06 2022_11 54 46_REC](https://user-images.githubusercontent.com/99672298/181744612-eb3d9fbd-1bce-4cd3-bf29-b2cc9d9daf03.png)
![29 06 2022_11 55 24_REC](https://user-images.githubusercontent.com/99672298/181744615-cce2a3af-048b-4852-b134-f691c87da5e7.png)
![29 06 2022_11 55 43_REC](https://user-images.githubusercontent.com/99672298/181744617-7d913019-01d3-4901-96fb-9519aa54e1a0.png)
![29 06 2022_11 56 09_REC](https://user-images.githubusercontent.com/99672298/181744620-492926e1-079e-471c-bb27-1e0d66ca96b0.png)
![29 06 2022_11 57 27_REC](https://user-images.githubusercontent.com/99672298/181744623-a6ecf67e-e6b2-4761-9d14-7d8f8d00f607.png)
![12 05 2022_19 15 24_REC](https://user-images.githubusercontent.com/99672298/181744946-8d3759b3-87a3-4053-98af-df5c6a894a4f.png)
![12 05 2022_19 15 41_REC](https://user-images.githubusercontent.com/99672298/181744987-bca3efb7-0ff6-43e3-ad21-f97b0c9e1f8a.png)
![12 05 2022_19 18 06_REC](https://user-images.githubusercontent.com/99672298/181745066-6f930ef2-7067-49a1-ab81-be169809be61.png)
![29 06 2022_12 19 31_REC](https://user-images.githubusercontent.com/99672298/181745412-42b15105-4057-4a1d-bb57-61a05d60915b.png)
![29 06 2022_12 33 18_REC](https://user-images.githubusercontent.com/99672298/181745438-b47586a6-1dc5-4c5e-8789-84fd3356fd4e.png)
![28 06 2022_12 58 57_REC](https://user-images.githubusercontent.com/99672298/181739963-a47dacc5-6947-4486-a88a-fdc8ead1d80d.png)

[Table of Content](#0.1)

### 2.7 Challenges with Gradient Descent<a class="anchor" id="2.7"></a>
___
Gradient Descent works fine in most of the cases, but there are many cases where gradient descent doesn't work properly or fails to work altogether

#### Gradient descent algorithm does not work for all functions. There are specific requirements. A function has to be:
+ **Continues variable and Differentiable**
  First, what does it mean it has to be differentiable?
If a function is differentiable it has a derivative for each point in its domain.not all functions meet these criteria. First, let’s see some examples of functions meeting this criterion:

![image](https://user-images.githubusercontent.com/99672298/181440157-886e7c5a-8d2e-466f-945d-b05fb784ac90.png)

Typical non-differentiable functions have a step a jump a cusp discontinuity of or infinte discontinuity:

![image](https://user-images.githubusercontent.com/99672298/181440208-9bd2365c-f18c-4e5b-bd3c-e2ccd34d2ca6.png)

+ **Next requirement — function has to be convex.**

![16 08 2022_11 50 49_REC](https://user-images.githubusercontent.com/99672298/186215840-4fe72b64-c559-45f0-964e-f08140590844.png)

#### Convex Functions
Geometrically, a function is convex if a line segment drawn from any point (x, f(x)) to another point (y, f(y)) -- called the chord from x to y -- lies on or above the graph of f, as in the picture below:

![image](https://user-images.githubusercontent.com/99672298/186218026-3fb092bd-4cad-4602-b85c-11c291e4712e.png)

Algebraically, f is convex if, for any x and y, and any t between 0 and 1, f( tx + (1-t)y ) <= t f(x) + (1-t) f(y).  A function is concave if -f is convex -- i.e. if the chord from x to y lies on or below the graph of f.  It is easy to see that every linear function -- whose graph is a straight line -- is both convex and concave.

#### A non-convex function "curves up and down" -- it is neither convex nor concave.  A familiar example is the sine function:

![image](https://user-images.githubusercontent.com/99672298/186218097-c413106c-7826-4b27-ac71-93f9586a064e.png)

![image](https://user-images.githubusercontent.com/99672298/181440345-5e8a10c9-0bd0-419f-8fb2-556d5c151384.png)

If the data is arranges in a way that it poses a non-convex optimization problem. It is very difficult to perform optimization problem. It is very difficult to perform
optimization using gradient descent. Gradient Descent only works for problems which have a well defined `convex optimization problems.`

Even when optimizing a convex optimization problem, there may be numerous minimal points. The lowest points is called `Global minima`, where as rest of the points ratger than the global minima are called local minima. Our main aim is go to the global minima avoiding local minima. There is also a **`Saddle Point`** problem. This is a point in the data where the gradient is zero but is not an optimal point. Whenever the slope of the cost function is at zero or just close to zero, the model stops learning further.

![image](https://user-images.githubusercontent.com/99672298/181446138-02faa76f-e083-47f6-b9c7-71a190d9449f.png)

Apart from the global minima, there occurs some scenarios that can show this slope, which is saddle Point and local minima generates the shape similar to the global minima, where the slope of the cost funcstions increase on both side of the current ponts. The name of the saddle pont is taken by that of a horse's saddle.

#### Another challenge

In a deep learning neural network often model is trained with gradient descent and back propagation there can occur two more issues other than lcoal minima and saddle points.

![image](https://user-images.githubusercontent.com/99672298/181450854-cca55386-f974-42e5-9d47-4c674050a5fd.png)
![26 07 2022_16 09 00_REC](https://user-images.githubusercontent.com/99672298/181470460-29085cba-cda1-4238-a4b0-e7591a57b1b2.png)

#### Vanishing and Exploding Gradients
___

These problems occur when the gradient is too large or too small and because of this problem the algorithms do no converge

![04 07 2022_20 05 34_REC](https://user-images.githubusercontent.com/99672298/181470768-e2af8e65-7b04-4f1b-ab99-f00162cc7930.png)

+ Vanishing Gradients:
Vanishing Gradient occurs when the gradient is smaller than expected. During backpropagation, this gradient becomes smaller that causing the decrease in the learning rate of earlier layers than the later layer of the network. Once this happens, the weight parameters update until they become insignificant.
+ Exploding Gradient:
Exploding gradient is just opposite to the vanishing gradient as it occurs when the Gradient is too large and creates a stable model. Further, in this scenario, model weight increases, and they will be represented as NaN. This problem can be solved using the dimensionality reduction technique, which helps to minimize complexity within the model.

![26 07 2022_16 09 30_REC](https://user-images.githubusercontent.com/99672298/181470534-006f49ed-3ce4-4e1f-a76c-fe5599a75ad9.png)

### 2.8 Types of Gradient Descent<a class="anchor" id="2.8"></a>
___
Based on the error in various training models, the Gradient Descent learning algorithm can be divided into Batch gradient descent, stochastic gradient descent, and mini-batch gradient descent. Let's understand these different types of gradient descent:

![26 07 2022_16 07 56_REC](https://user-images.githubusercontent.com/99672298/181470298-c33c0863-7914-41ff-90ac-b06fad97cea4.png)

#### **Batch Gardient Descent**
___
Batch gradient descent (BGD) is used to find the error for each point in the training set and update the model after evaluating all training examples. This procedure is known as the training **`epoch.`** In simple words, it is a greedy approach where we have to sum over all examples for each update.

Advantages of Batch gradient descent:
+ It produces less noise in comparison to other gradient descent.
+ It produces stable gradient descent convergence.
+ It is Computationally efficient as all resources are used for all training samples.

Disadvantages of Batch gradient descent:
+ Sometimes a stable error gradient can lead to a local minima and unlike stochastic gradient descent no noisy steps are there to help get out of the local minima
+ The entire training set can be too large to process in the memory due to which additional memory might be needed
+ Depending on computer resources it can take too long for processing all the training samples as a batch

#### **Stochastic gradient descent**
___
![29 06 2022_12 34 35_REC](https://user-images.githubusercontent.com/99672298/181745492-c0b3afb7-cb68-4893-9eba-5f0bfeff9236.png)

So there is a thing called Stochastic Gradient Descent that uses a randomly selected subset of the data at every step rather than the full dataset. This reduces the time spent calculating the derivatives of the Loss function.

Stochastic gradient descent (SGD) is a type of gradient descent that runs one training example per iteration. Or in other words, it processes a training epoch for each example within a dataset and updates each training example's parameters one at a time. As it requires only one training example at a time, hence it is easier to store in allocated memory. However, it shows some computational efficiency losses in comparison to batch gradient systems as it shows frequent updates that require more detail and speed. 

Further, due to frequent updates, it is also treated as a noisy gradient. However, sometimes it can be helpful in finding the global minimum and also escaping the local minimum.

Advantages of Stochastic gradient descent:

In Stochastic gradient descent (SGD), learning happens on every example, and it consists of a few advantages over other gradient descent.

+ It is easier to allocate in desired memory.
+ It is relatively fast to compute than batch gradient descent.
+ It is more efficient for large datasets.

Disadvantages of Stochastic Gradient descent:

+ Updating the model so frequently is more computationally expensive than other configurations of gradient descent, taking significantly longer to train models on large datasets.
+ The frequent updates can result in a noisy gradient signal, which may cause the model parameters and in turn the model error to jump around (have a higher variance over training epochs).
+ The noisy learning process down the error gradient can also make it hard for the algorithm to settle on an error minimum for the model.

![image](https://user-images.githubusercontent.com/99672298/181701953-5b86bd6b-e290-46bf-9602-22eb201cde57.png)
![02 07 2022_12 14 04_REC](https://user-images.githubusercontent.com/99672298/181738300-3a2a2ffb-880e-44c6-842d-eb978775f8f1.png)

#### **MiniBatch Gradient Descent:**
___

![04 07 2022_14 54 15_REC](https://user-images.githubusercontent.com/99672298/181737881-7dd5b705-2c20-49d2-a8ee-810745013a9e.png)

Mini Batch gradient descent is the combination of both batch gradient descent and stochastic gradient descent. It divides the training datasets into small batch sizes then performs the updates on those batches separately. 

Splitting training datasets into smaller batches make a balance to maintain the computational efficiency of batch gradient descent and speed of stochastic gradient descent. Hence, we can achieve a special type of gradient descent with higher computational efficiency and less noisy gradient descent.

![29 06 2022_12 35 31_REC](https://user-images.githubusercontent.com/99672298/181746128-55005f6e-a1d3-4d22-9c44-6b5927e345f0.png)
![29 06 2022_12 35 09_REC](https://user-images.githubusercontent.com/99672298/181746139-9ba5de7d-ef81-4e86-9302-8756714985f8.png)
![29 06 2022_12 34 52_REC](https://user-images.githubusercontent.com/99672298/181746161-16650553-15b0-4935-86f4-c1f964740e6e.png)

Advantages of Mini Batch gradient descent:

+ It is easier to fit in allocated memory.
+ It is computationally efficient.
+ It produces stable gradient descent convergence.

![29 06 2022_12 35 52_REC](https://user-images.githubusercontent.com/99672298/181746223-cc6c98ac-9484-467a-8250-40dcb32c6867.png)
![29 06 2022_12 36 14_REC](https://user-images.githubusercontent.com/99672298/181746244-54ca7426-799c-4b5e-b76b-53b9463d6967.png)
![1_xtdBbCo-4iDMWim4R49JVg](https://user-images.githubusercontent.com/99672298/181737797-11f2b578-c9d5-4e1c-82cd-5fa4670442e8.png)
![1_OwX5ky1lqycOIH2LiwSCyQ](https://user-images.githubusercontent.com/99672298/181737758-4dfb1c80-5455-4bcf-9cfb-91dafb191d94.png)
![02 07 2022_11 45 36_REC](https://user-images.githubusercontent.com/99672298/181738253-0cd9e1f3-7f2d-415c-94e7-d1920cfbcf1a.png)
![28 06 2022_22 45 47_REC](https://user-images.githubusercontent.com/99672298/181740448-fa7de855-4ed7-4e9a-9f42-61e319c3f3e9.png)
![28 06 2022_23 19 49_REC](https://user-images.githubusercontent.com/99672298/181740549-16bbb914-d89d-4c5d-91df-d35a9bb55c8b.png)

#### Drawbacks of base optimizer:(GD, SGD, mini-batch GD)

+ **Gradient Descent uses the whole training data to update weight and bias. Suppose if we have millions of records then training becomes slow and computationally very expensive.**
+ **SGD solved the Gradient Descent problem by using only single records to updates parameters. But, still, SGD is slow to converge because it needs forward and backward propagation for every record. And the path to reach global minima becomes very noisy.**
+ **Mini-batch GD overcomes the SDG drawbacks by using a batch of records to update the parameter. Since it doesn't use entire records to update parameter, the path to reach global minima is not as smooth as Gradient Descent.**

![image](https://user-images.githubusercontent.com/99672298/186222534-d6e0977d-15a3-40ed-8865-0d847dbb7439.png)

The above figure is the plot between the number of epoch on the x-axis and the loss on the y-axis. We can clearly see that in Gradient Descent the loss is reduced smoothly whereas in SGD there is a high oscillation in loss value.

[Table of Content](#0.1)

### 2.9 Variants of Gradient Descent Algorithm<a class="anchor" id="2.9"></a>
___

#### **Vanilla Gradient Descent**
___
This is the simplest form of gradient descent technique. Here, vanilla means pure / without any adulteration. Its main feature is that we take small steps in the direction of the minima by taking gradient of the cost function.

Let’s look at its pseudocode.
+ update = learning_rate * gradient_of_parameters
+ parameters = parameters - update

Here, we see that we make an update to the parameters by taking gradient of the parameters. And multiplying it by a learning rate, which is essentially a constant number suggesting how fast we want to go the minimum. Learning rate is a hyper-parameter and should be treated with care when choosing its value.

![image](https://user-images.githubusercontent.com/99672298/181469887-dd53f973-c13c-42d9-bcd8-a32f5cfc2f84.png)

#### **Gradient Descent with Momentum**
___

![28 06 2022_16 18 21_REC](https://user-images.githubusercontent.com/99672298/181740272-71c61c55-ad5e-4d2c-b2b0-601d76197ebd.png)

Here, we tweak the above algorithm in such a way that we pay heed to the prior step before taking the next step.

Here’s a pseudocode.
+ update = learning_rate * gradient
+ velocity = previous_update * momentum
+ parameter = parameter + velocity – update

Here, our update is the same as that of vanilla gradient descent. But we introduce a new term called velocity, which considers the previous update and a constant which is called momentum.

![image](https://user-images.githubusercontent.com/99672298/181737688-bd1dd8fc-cd39-4248-a9c7-d939e3829a37.png)

#### **ADAGRAD**
___
ADAGRAD uses adaptive technique for learning rate updation. In this algorithm, on the basis of how the gradient has been changing for all the previous iterations we try to change the learning rate.

Here’s a pseudocode
+ grad_component = previous_grad_component + (gradient * gradient)
+ rate_change = square_root(grad_component) + epsilon
+ adapted_learning_rate = learning_rate * rate_change
+ update = adapted_learning_rate * gradient
+ parameter = parameter – update
#### **ADAM**
___
ADAM is one more adaptive technique which builds on adagrad and further reduces it downside. In other words, you can consider this as momentum + ADAGRAD.

Here’s a pseudocode.

+ adapted_gradient = previous_gradient + ((gradient – previous_gradient) * (1 – beta1))
+ gradient_component = (gradient_change – previous_learning_rate)
+ adapted_learning_rate =  previous_learning_rate + (gradient_component * (1 – beta2))
+ update = adapted_learning_rate * adapted_gradient
+ parameter = parameter – update
+ Here beta1 and beta2 are constants to keep changes in gradient and learning rate in check

### The problem with gradient descent is that the weight update at a moment (t) is governed by the learning rate and gradient at that moment only. It doesn't take into account the past steps.
___

It leads to the following problems:

1.) The Saddle point Problem (plateau)

![image](https://user-images.githubusercontent.com/99672298/181585064-594d61de-cc66-459b-ad54-dd082396a133.png)

2.) Noisy - The path followed by the Gradient descent

![image](https://user-images.githubusercontent.com/99672298/181584434-6b0f391e-a021-4f1e-88db-a4dd72e68839.png)
![](https://miro.medium.com/max/992/1*t-kykynrtQ0olmFeNgIB0w.gif)

A problem with the gradient descent algorithm is that the progression of the search space based on the gradient. For example, the search may progress downhill towards the minima, but during this progression, it may move in another direction, even uphill, this can slow down the progress of the search.

![image](https://user-images.githubusercontent.com/99672298/181585689-2b0cd426-4425-413e-9f89-bc9c4d646c05.png)

Another prblem let's assume the intial weight of the network under consideration corresponds to point 'P1' (Look at the below figure)  with gradient descent, the loss function decreases rapidly along the slope 'P1' to 'P2' as the gradient along this slope is high. But as soon as it reaches 'P2' the gradient becomes very low. The weight updates around 'P2' is very small, Even after many iterations, the cost moves very slowly before getting stuck at a point where the gradient eventually becomes zero. In the below case as you can see in the figure, ideally cost should have moved to the global minima point 'P3' but because the gradient disappear at point 'B', we are stuck

![image](https://user-images.githubusercontent.com/99672298/181586827-0e55e9f5-9372-4344-8dfb-b44b32d8ce17.png)

One approach to the problem is to add history to the parameter update equation based on the gradient encountered in the previous updates. 

"If I am repeatedly being asked to move in the same direction then I should probably gain some confidence and start taking bigger steps in that direction. Just as a ball gains momentum while rolling down a slope." This changes is based on the metaphor of momentum from physics where accelaration in a direction can be acculmulated from past updates.

### Momentum
___
Momentum is an extension to the gradient descent optimization algorithm, often referred to as gradient descent with momentum.
#### How come momentum is going to help us fix our earlier two problems?

#### 1.) Saddle point problem 

#### 2.) Noisy path followed

![image](https://user-images.githubusercontent.com/99672298/181620407-5b9bbd7f-7f51-4747-b644-fcc002586100.png)

Now, Imagine you have a ball rolling from point A. The ball starts rolling down slowly and gathers some momentum across the slope AB. When the ball reaches point B, it has accumulated enough momentum to push itself across the plateau region B and finally following slope BC to land at the global minima C.

#### How can this be used and applied to Gradient Descent?
We can use a moving average over the past gradients, it also helps reduce the noise in each iteration using Momentum on top of the Gradient Descent. In regions where the gradient is high like AB, weight updates will be large. Thus, in a way we are gathering momentum by taking a moving average over these gradients.

### SGD with momentum
It always works better than the normal Stochastic Gradient Descent Algorithm. The problem with SGD is that while it tries to reach minima because of the high oscillation we can’t increase the learning rate. So it takes time to converge. In this algorithm, we will be using Exponentially Weighted Averages to compute Gradient and used this Gradient to update parameter.

+ An equation to update weights and bias in SGD

![image](https://user-images.githubusercontent.com/99672298/186223548-f44fa28e-168c-4e50-a883-c711b3497596.png)

+ An equation to update weights and bias in SGD with momentum

![image](https://user-images.githubusercontent.com/99672298/186223648-2c0d9fb4-9d5c-4d4d-998d-d025319d04d9.png)

But there is a problem with this method, it considers all the gradients over iterations with equal weightage. The gradient at t=0 has equal weightage as that of the gradient at current iteration t. We need to use some sort of weighted average of the past gradients such that the recent gradients are given more weightage.

This can be done by using an Exponential Moving Average(EMA). An exponential moving average is a moving average that assigns a greater weight on the most recent values.

#### **`Exponentially Weighted Averages`** is used in sequential noisy data to reduce the noise and smoothen the data. To denoise the data, we can use the following equation to generate a new sequence of data with less noise.

![image](https://user-images.githubusercontent.com/99672298/186223800-cd957a3a-c4db-4513-9f7b-51cee2df5bf5.png)
![image](https://user-images.githubusercontent.com/99672298/186223923-b4997e75-f0b5-4a8b-89c5-a529c9726b72.png)

Now, let’s see how the new sequence is generated using the above equation: For our example to make it simple, let’s consider a sequence of size 3.

![image](https://user-images.githubusercontent.com/99672298/186224028-cdb0658a-622b-460f-8c2d-0539a4aed90a.png)

Let’s expand V3 equation:

![image](https://user-images.githubusercontent.com/99672298/186224075-58fe6497-3e7d-467a-886f-b20aa105ac2c.png)

From the above equation, at time step t=3 more weightage is given to a3(which is the latest generated data) then followed by a2 previously generated data, and so on. This is how the sequence of noisy data is smoothened. It works better in a long sequence because, in the initial period, the averaging effect is less due to fewer data points.

**`Momentum can be interpreted as a ball rolling down a nearly horizontal incline. The ball naturally gathers momentum as gravity causes it to accelerate.`**

This to some amount addresses our second problem. Gradient Descent with Momentum takes small steps in directions where the gradients oscillate and take large steps along the direction where the past gradients have the same direction(same sign). This problem with momentum is that acceleration can sometimes overshoot the search and run past our goal other side of the minima valley. While making a lot og U-turns before finally converging.

#### Can we do something to reduce the oscillation/ U-turns / overshooting the minima?
#### YES!

### Nesterov Momentum
___

![image](https://user-images.githubusercontent.com/99672298/181622949-fd237ff6-6edb-49d9-b00f-5667c348e2b4.png)

A limitation of gradient descent is that it can get stuck in flat areas or bounce around if the objective function returns noisy gradients. Momentum is an approach that accelerates the progress of the search to skim across flat areas and smooth out bouncy gradients.

In some cases, the acceleration of momentum can cause the search to miss or overshoot the minima at the bottom of basins or valleys. Nesterov momentum is an extension of momentum that involves calculating the decaying moving average of the gradients of projected positions in the search space rather than the actual positions themselves.

While `Momentum` first computes the current gradient and then take a big jump in the direction of the updated accumulated gradient, where **`Nesterov`** first makes a big jump in the direction of the previous accumulated gradient, measures the gradient and then complete Nesterov update. This anticipatory updates  prevents us from going to fast and results in increased responsiveness and reduces oscillation.

This has the effect of harnessing the accelerating benefits of momentum whilst allowing the search to slow down when approaching the optima and reduce the likelihood of missing or overshooting it.

![image](https://user-images.githubusercontent.com/99672298/181702525-3eb51256-3255-4035-b540-5c13648a3560.png)

**`Look ahead before you leap`**

### Adaptive Gradient Descent (ADAGrad)
___

A problem with the gradient descent algorithm is that the step size (learning rate) is the same for each variable or dimension in the search space. It is possible that better performance can be achieved using a step size that is tailored to each variable, allowing larger movements in dimensions with a consistently steep gradient and smaller movements in dimensions with less steep gradients.

The idea behind Adagrad is to use different learning rates for each parameter base on iteration. The reason behind the need for different learning rates is that the learning rate for sparse features parameters needs to be higher compare to the dense features parameter because the frequency of occurrence of sparse features is lower.

Equation:

![image](https://user-images.githubusercontent.com/99672298/186224327-345708cd-3bc6-446f-a7a2-d2d1dab9802e.png)

In the above Adagrad optimizer equation, the learning rate has been modified in such a way that it will automatically decrease because the summation of the previous gradient square will always keep on increasing after every time step.
Now, let’s take a simple example to check how the learning rate is different for every parameter in a single time step. For this example, we will consider a single neuron with 2 inputs and 1 output. So, the total number of parameters will be 3 including bias.

![image](https://user-images.githubusercontent.com/99672298/186224603-fc766200-b779-4e17-a005-3fd55647e80a.png)

The above computation is done at a single time step, where all the three parameters learning rate “η” is divided by the square root of “α” which is different for all parameters. So, we can see that the learning rate is different for all three parameters.

Now, let’s see how weights and bias are updated in Stochastic Gradient Descent.

![image](https://user-images.githubusercontent.com/99672298/186224673-289666c2-b8b6-4d47-b812-fd457db0ff82.png)

Similarly, the above computation is done at a single time step, and here the learning rate “η” remains the same for all parameters.

Lastly, despite not having to manually tune the learning rate there is one huge disadvantage i.e due to monotonically decreasing learning rates, at some point in time step, the model will stop learning as the learning rate is almost close to 0.

AdaGrad is designed to specifically explore the idea of automatically tailoring the step size for each dimension in the search space.

An internal variable is then maintained for each input variable that is the sum of the squared partial derivatives for the input variable observed during the search.

This sum of the squared partial derivatives is then used to calculate the step size for the variable by dividing the initial step size value (e.g. hyperparameter value specified at the start of the run) divided by the square root of the sum of the squared partial derivatives.

One of Adagrad’s main benefits is that it eliminates the need to manually tune the learning rate. But, Adagrad’s main weakness is its accumulation of the squared gradients in the denominator: Since every added term is positive, the accumulated sum keeps growing during training. This in turn causes the learning rate to shrink and eventually become infinitesimally small, at which point the algorithm is no longer able to acquire additional knowledge. This has the effect of stopping the search too soon, before the minima can even be located.

**`Adaptive Gradients, or AdaGrad for short, is an extension of the gradient descent optimization algorithm that allows the step size in each dimension used by the optimization algorithm to be automatically adapted based on the gradients seen for the variable (partial derivatives) seen over the course of the search.`**

## Root Mean Squared Propogation (RMSProp)
___
Root Mean Squared Propagation, or RMSProp, is an extension of gradient descent and the AdaGrad version of gradient descent that uses a decaying average of partial gradients in the adaptation of the step size for each parameter. 

The use of a decaying moving average allows the algorithm to forget early gradients and focus on the most recently observed partial gradients seen during the progress of the search, overcoming the limitation of AdaGrad.

RMSProp is designed to accelerate the optimization process, e.g. decrease the number of function evaluations required to reach the optima, or to improve the capability of the optimization algorithm, e.g. result in a better final result.

It is related to another extension to gradient descent called Adaptive Gradient, or AdaGrad.

AdaGrad is designed to specifically explore the idea of automatically tailoring the step size (learning rate) for each parameter in the search space. This is achieved by first calculating a step size for a given dimension, then using the calculated step size to make a movement in that dimension using the partial derivative. This process is then repeated for each dimension in the search space.

Adagrad calculates the step size for each parameter by first summing the partial derivatives for the parameter seen so far during the search, then dividing the initial step size hyperparameter by the square root of the sum of the squared partial derivatives.

AdaGrad shrinks the learning rate according to the entire history of the squared gradient and may have made the learning rate too small before arriving at such a convex structure.

**`RMSProp extends Adagrad to avoid the effect of a monotonically decreasing learning rate.`**

RMSProp can be thought of as an extension of AdaGrad in that it uses a decaying average or moving average of the partial derivatives instead of the sum in the calculation of the learning rate for each parameter.

This is achieved by adding a new hyperparameter we will call rho that acts like momentum for the partial derivatives.

RMSProp maintains a decaying average of squared gradients.

Using a decaying moving average of the partial derivative allows the search to forget early partial derivative values and focus on the most recently seen shape of the search space.

RMSProp uses an exponentially decaying average to discard history from the extreme past so that it can converge rapidly after finding a convex bowl, as if it were an instance of the AdaGrad algorithm initialized within that bowl.

The RMSprop optimizer is similar to the gradient descent algorithm with momentum. The RMSprop optimizer restricts the oscillations in the vertical direction. Therefore, we can increase our learning rate and our algorithm could take larger steps in the horizontal direction converging faster. The difference between RMSprop and gradient descent is on how the gradients are calculated.

RMSprop and Adadelta have both been developed independently around the same time stemming from the need to resolve Adagrad’s radically diminishing learning rates. RMSprop divides the learning rate by an exponentially decaying average of squared gradients.

![image](https://user-images.githubusercontent.com/99672298/181702611-58176549-a318-440b-a68c-2ed9144efc2f.png)

### Ada-Delta
___

A limitation of gradient descent is that it uses the same step size (learning rate) for each input variable. AdaGradn and RMSProp are extensions to gradient descent that add a self-adaptive learning rate for each parameter for the objective function.

Adadelta can be considered a further extension of gradient descent that builds upon AdaGrad and RMSProp and changes the calculation of the custom step size so that the units are consistent and in turn no longer requires an initial learning rate hyperparameter.

Adadelta is designed to accelerate the optimization process, e.g. decrease the number of function evaluations required to reach the optima, or to improve the capability of the optimization algorithm, e.g. result in a better final result.

It is best understood as an extension of the AdaGrad and RMSProp algorithms.

AdaGrad is an extension of gradient descent that calculates a step size (learning rate) for each parameter for the objective function each time an update is made. The step size is calculated by first summing the partial derivatives for the parameter seen so far during the search, then dividing the initial step size hyperparameter by the square root of the sum of the squared partial derivatives.

RMSProp can be thought of as an extension of AdaGrad in that it uses a decaying average or moving average of the partial derivatives instead of the sum in the calculation of the step size for each parameter. This is achieved by adding a new hyperparameter “rho” that acts like a momentum for the partial derivatives.

Adadelta is a further extension of RMSProp designed to improve the convergence of the algorithm and to remove the need for a manually specified initial learning rate.

The idea presented in this paper was derived from ADAGRAD in order to improve upon the two main drawbacks of the method: 1) the continual decay of learning rates throughout training, and 2) the need for a manually selected global learning rate.

The decaying moving average of the squared partial derivative is calculated for each parameter, as with RMSProp. The key difference is in the calculation of the step size for a parameter that uses the decaying average of the delta or change in parameter.

This choice of numerator was to ensure that both parts of the calculation have the same units.

After independently deriving the RMSProp update, the authors noticed that the units in the update equations for gradient descent, momentum and Adagrad do not match. To fix this, they use an exponentially decaying average of the square updates

Adadelta is an extension of Adagrad that seeks to reduce its aggressive, monotonically decreasing learning rate. Instead of accumulating all past squared gradients, Adadelta restricts the window of accumulated past gradients to some fixed size. The idea behind Adadelta is that instead of summing up all the past squared gradients from 1 to “t” time steps, what if we could restrict the window size. For example, computing the squared gradient of the past 10 gradients and average out. This can be achieved using Exponentially Weighted Averages over Gradient.

![image](https://user-images.githubusercontent.com/99672298/186225170-04c034db-2cd4-4a51-af32-e0050e2d077c.png)

The above equation shows that as the time steps “t” increase the summation of squared gradients “α” increases which led to a decrease in learning rate “η”. In order to resolve the exponential increase in the summation of squared gradients “α”, we replaced the “α” with exponentially weighted averages of squared gradients.

![image](https://user-images.githubusercontent.com/99672298/186225246-9e4dff86-841d-4043-98b8-61b080ae387d.png)

So, here unlike the alpha “α” in Adagrad, where it increases exponentially after every time step. In Adadelda, using the exponentially weighted averages over the past Gradient, an increase in “Sdw” is under control. The calculation for “Sdw” is similar to the example I did in the Exponentially Weighted Averages section.

The typical “β” value is 0.9 or 0.95.

### Adaptive Movement Estimation (ADAM)
___

Adam optimizer is by far one of the most preferred optimizers. The idea behind Adam optimizer is to utilize the momentum concept from “SGD with momentum” and adaptive learning rate from “Ada delta”.

The Adaptive Movement Estimation or ADAM for short is an extension to gradient and a natural successor to technique like Adagrad and RMSProp that automatically adapts a learning rate for each input varibale for the objective function and further smoothens the search process by using an exponentially decreasing moving average of the gradient.

This involves maintaining a first and second moment of the gradient that is an exponentially decaying mean gradient and variance for each input variables.

Adam can be described as a combination of two other extention of Stochastic gradient descent.

The two combined advantages come from 

1.) Adaptive Gradient Algorithm (AdaGrad) that maintains a per-parameter learning rate that improves performance on problems with sparse gradients (e.g. natural language and computer vision problems).

2.) Root Mean Square Propagation (RMSProp) that also maintains per-parameter learning rates that are adapted based on the average of recent magnitudes of the gradients for the weight (e.g. how quickly it is changing). This means the algorithm does well on online and non-stationary problems (e.g. noisy).

also

**`Exponential Weighted Averages for past gradients`**

![image](https://user-images.githubusercontent.com/99672298/186225708-789e9b1e-bc24-469a-8fab-7ff0bcf79868.png)

**`Exponential Weighted Averages for past squared gradients`**

![image](https://user-images.githubusercontent.com/99672298/186225758-3d4ecd2c-44b6-4500-a587-4a8684abbb99.png)

Using the above equation, now the weight and bias updation formula looks like:

![image](https://user-images.githubusercontent.com/99672298/186225808-50c853f8-84a6-4d71-8a63-4bdf842fc5a9.png)


Adam bears the fruits from both world AdaGrad and RMSProp. In addition to storing an exponentially decaying average of past squared gradients, Adam also keeps an exponentially decaying average of past gradients similar to momentum.

![image](https://user-images.githubusercontent.com/99672298/181702663-3976e135-3b23-4907-83f6-5f517089d7f9.png)

![image](https://user-images.githubusercontent.com/99672298/181701433-ff0bf689-5424-4bfa-8e19-6d7ce5a6831c.png)

### Nesterov Accelerated Adaptive Moment Estimation (NADAM)
___

![image](https://user-images.githubusercontent.com/99672298/181702035-ce939619-f028-4ca9-b6c5-7178617b0259.png)

As we know by now, which the limitation of gradient descent is the progess of the search can slow down if the gradient becomes flat or large curvature. Momentum was added to gradient descent that incorporates some inertia to overshoot the problem. Some times overshoot can be a problem which can be further improved by incorporating the gradient to project new position rather than the current position looking at the future rather than the past like Momentum, called as Nesterov's Accelerated Gradient.

Another limitation of gradient descent is that a single step size (learning rate) is used for all input variables. Extensions to gradient descent like the Adaptive Movement Estimation (Adam) algorithm that uses a separate step size for each input variable but may result in a step size that rapidly decreases to very small values.

Nesterov-accelerated Adaptive Moment Estimation, or the Nadam, is an extension of the Adam algorithm that incorporates Nesterov momentum and can result in better performance of the optimization algorithm.

ADAM is an extension of gradient descent that adds a first and second moment of the gradient and automatically adapts a learning rate for each parameter that is being optimized. NAG is an extension to momentum where the update is performed using the gradient of the projected update to the parameter rather than the actual current variable value. This has the effect of slowing down the search when the optima is located rather than overshooting, in some situations.

![image](https://user-images.githubusercontent.com/99672298/181702773-71ff0115-0df7-4892-a800-c8c974d7642c.png)
![28 06 2022_16 38 22_REC](https://user-images.githubusercontent.com/99672298/186171175-dbbad1c0-788b-4183-ae74-bf8868b48c93.png)

There is something called bias correction while using Exponential Weighted Averages. Bias correction is used to get a better estimate in the initial time steps. But often most people don’t bother to implement bias correction because most people would rather wait for an initial period and then after some time steps the bias error will become insignificant.

[Table of Content](#0.1)

### 3 Overview:<a class="anchor" id="3"></a>
___
Gradient descent refers to a minimization optimization algorithm that follows the negative of the gradient downhill of the target function to locate the minimum of the function.

![26 07 2022_16 07 35_REC](https://user-images.githubusercontent.com/99672298/181737475-8d1251ee-815e-41c8-8e56-7413f71f0b5f.png)

![](https://miro.medium.com/max/1400/0*oqm7QVnI9-inFGCc.gif)

A downhill movement is made by first calculating how far to move in the input space, calculated as the steps size (called alpha or the learning rate) multiplied by the gradient. This is then subtracted from the current point, ensuring we move against the gradient, or down the target function.

The steeper the objective function at a given point, the larger the magnitude of the gradient, and in turn, the larger the step taken in the search space. The size of the step taken is scaled using a step size hyperparameter.
+ Step Size (alpha): Hyperparameter that controls how far to move in the search space against the gradient each iteration of the algorithm.
+ Gradient descent is an optimization algorithm that follows the negative gradient of an objective function in order to locate the minimum of the function.

A downhill movement is made by first calculating how far to move in the input space, calculated as the steps size (called alpha or the learning rate) multiplied by the gradient. This is then subtracted from the current point, ensuring we move against the gradient, or down the target function.

x(t+1) = x(t) – step_size * f'(x(t))

![26 07 2022_16 07 12_REC](https://user-images.githubusercontent.com/99672298/181737533-465351c9-ee18-4a79-b6a9-2f222fd96cc9.png)

The steeper the objective function at a given point, the larger the magnitude of the gradient, and in turn, the larger the step taken in the search space. The size of the step taken is scaled using a step size hyperparameter.

Step Size (alpha): Hyperparameter that controls how far to move in the search space against the gradient each iteration of the algorithm.
If the step size is too small, the movement in the search space will be small, and the search will take a long time. If the step size is too large, the search may bounce around the search space and skip over the optima.

![29 06 2022_12 20 14_REC](https://user-images.githubusercontent.com/99672298/181745213-8a536a87-7245-4365-b67c-de6df086d26b.png)

___

## Author

<table>
<tr>
<td>
     <img src="https://avatars.githubusercontent.com/u/132883342?v=4" width="180"/>
     
     saifiansari17@gmail.com

<p align="center">
<a href = "https://github.com/SAIFIANS"><img src = "http://www.iconninja.com/files/241/825/211/round-collaboration-social-github-code-circle-network-icon.svg" width="36" height = "36"/></a>
<a href = "https://www.linkedin.com/in/mohammad-saifi-ansari//"><img src = "http://www.iconninja.com/files/863/607/751/network-linkedin-social-connection-circular-circle-media-icon.svg" width="36" height="36"/></a>
</p>
</td>
</tr> 
  </table>

[Table of Content](#0.1)

<div style="display:fill;
            border-radius: false;
            border-style: solid;
            border-color:#000000;
            border-style: false;
            border-width: 2px;
            color:#CF673A;
            font-size:15px;
            font-family: Georgia;
            background-color:#E8DCCC;
            text-align:center;
            letter-spacing:0.1px;
            padding: 0.1em;">

**<h2>♡ Thank you for taking the time ♡**
