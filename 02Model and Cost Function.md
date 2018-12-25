![image-20181225125209002](assets/image-20181225125209002-5713529.png)

# Model Representation

To establish notation for future use, we’ll use x^{(i)}x(i) to denote the “input” variables (living area in this example), also called input features, and y^{(i)}y(i) to denote the “output” or target variable that we are trying to predict (price). A pair (x^{(i)} , y^{(i)} )(x(i),y(i)) is called a training example, and the dataset that we’ll be using to learn—a list of m training examples {(x^{(i)} , y^{(i)} ); i = 1, . . . , m}—is called a training set. Note that the superscript “(i)” in the notation is simply an index into the training set, and has nothing to do with exponentiation. We will also use X to denote the space of input values, and Y to denote the space of output values. In this example, X = Y = ℝ.

To describe the supervised learning problem slightly more formally, our goal is, given a training set, to learn a function h : X → Y so that h(x) is a “good” predictor for the corresponding value of y. For historical reasons, this function h is called a hypothesis. Seen pictorially, the process is therefore like this:

![img](assets/H6qTdZmYEeaagxL7xdFKxA_2f0f671110e8f7446bb2b5b2f75a8874_Screenshot-2016-10-23-20.14.58-20181225130423783.png)

When the target variable that we’re trying to predict is continuous, such as in our housing example, we call the learning problem a regression problem. When y can take on only a small number of discrete values (such as if, given the living area, we wanted to predict if a dwelling is a house or an apartment, say), we call it a classification problem.



# Cost Function

We can measure the accuracy of our hypothesis function by using a **cost function**. This takes an average difference (actually a fancier version of an average) of all the results of the hypothesis with inputs from x's and the actual output y's.

J(\theta_0, \theta_1) = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left ( \hat{y}_{i}- y_{i} \right)^2 = \dfrac {1}{2m} \displaystyle \sum _{i=1}^m \left (h_\theta (x_{i}) - y_{i} \right)^2J(θ0,θ1)=2m1i=1∑m(y^i−yi)2=2m1i=1∑m(hθ(xi)−yi)2

To break it apart, it is \frac{1}{2}21 \bar{x}xˉ where \bar{x}xˉ is the mean of the squares of h_\theta (x_{i}) - y_{i}hθ(xi)−yi , or the difference between the predicted value and the actual value.

This function is otherwise called the "Squared error function", or "Mean squared error". The mean is halved \left(\frac{1}{2}\right)(21) as a convenience for the computation of the gradient descent, as the derivative term of the square function will cancel out the \frac{1}{2}21term. The following image summarizes what the cost function does:

![img](assets/R2YF5Lj3EeajLxLfjQiSjg_110c901f58043f995a35b31431935290_Screen-Shot-2016-12-02-at-5.23.31-PM.png)



# Cost Function - Intuition I

If we try to think of it in visual terms, our training data set is scattered on the x-y plane. We are trying to make a straight line (defined by h_\theta(x)hθ(x)) which passes through these scattered data points.

Our objective is to get the best possible line. The best possible line will be such so that the average squared vertical distances of the scattered points from the line will be the least. Ideally, the line should pass through all the points of our training data set. In such a case, the value of J(\theta_0, \theta_1)J(θ0,θ1) will be 0. The following example shows the ideal situation where we have a cost function of 0.

![img](assets/_B8TJZtREea33w76dwnDIg_3e3d4433e32478f8df446d0b6da26c27_Screenshot-2016-10-26-00.57.56.png)

When \theta_1 = 1θ1=1, we get a slope of 1 which goes through every single data point in our model. Conversely, when \theta_1 = 0.5θ1=0.5, we see the vertical distance from our fit to the data points increase.

![img](assets/8guexptSEeanbxIMvDC87g_3d86874dfd37b8e3c53c9f6cfa94676c_Screenshot-2016-10-26-01.03.07.png)

This increases our cost function to 0.58. Plotting several other points yields to the following graph:

![img](assets/fph0S5tTEeajtg5TyD0vYA_9b28bdfeb34b2d4914d0b64903735cf1_Screenshot-2016-10-26-01.09.05.png)

Thus as a goal, we should try to minimize the cost function. In this case, \theta_1 = 1θ1=1 is our global minimum.



**首先计算每个parameter的更新值，然后同时更新所有parameter的值。**



# Gradient Descent

So we have our hypothesis function and we have a way of measuring how well it fits into the data. Now we need to estimate the parameters in the hypothesis function. That's where gradient descent comes in.

Imagine that we graph our hypothesis function based on its fields \theta_0θ0 and \theta_1θ1 (actually we are graphing the cost function as a function of the parameter estimates). We are not graphing x and y itself, but the parameter range of our hypothesis function and the cost resulting from selecting a particular set of parameters.

We put \theta_0θ0 on the x axis and \theta_1θ1 on the y axis, with the cost function on the vertical z axis. The points on our graph will be the result of the cost function using our hypothesis with those specific theta parameters. The graph below depicts such a setup.

![img](assets/bn9SyaDIEeav5QpTGIv-Pg_0d06dca3d225f3de8b5a4a7e92254153_Screenshot-2016-11-01-23.48.26.png)

We will know that we have succeeded when our cost function is at the very bottom of the pits in our graph, i.e. when its value is the minimum. The red arrows show the minimum points in the graph.

The way we do this is by taking the derivative (the tangential line to a function) of our cost function. The slope of the tangent is the derivative at that point and it will give us a direction to move towards. We make steps down the cost function in the direction with the steepest descent. The size of each step is determined by the parameter α, which is called the learning rate.

For example, the distance between each 'star' in the graph above represents a step determined by our parameter α. A smaller α would result in a smaller step and a larger α results in a larger step. The direction in which the step is taken is determined by the partial derivative of J(\theta_0,\theta_1)J(θ0,θ1). Depending on where one starts on the graph, one could end up at different points. The image above shows us two different starting points that end up in two different places.

The gradient descent algorithm is:

repeat until convergence:

![image-20181225133906692](assets/image-20181225133906692-5716346.png)

where

j=0,1 represents the feature index number.

At each iteration j, one should simultaneously update the parameters \theta_1, \theta_2,...,\theta_nθ1,θ2,...,θn. Updating a specific parameter prior to calculating another one on the j^{(th)}j(th) iteration would yield to a wrong implementation.

![img](assets/yr-D1aDMEeai9RKvXdDYag_627e5ab52d5ff941c0fcc741c2b162a0_Screenshot-2016-11-02-00.19.56.png)

\theta_1:=\theta_1-\alpha * 0θ1:=θ1−α∗0

# Gradient Descent Intuition

In this video we explored the scenario where we used one parameter \theta_1θ1 and plotted its cost function to implement a gradient descent. Our formula for a single parameter was :

Repeat until convergence:

\theta_1:=\theta_1-\alpha \frac{d}{d\theta_1} J(\theta_1)θ1:=θ1−αdθ1dJ(θ1)

Regardless of the slope's sign for \frac{d}{d\theta_1} J(\theta_1)dθ1dJ(θ1), \theta_1θ1 eventually converges to its minimum value. The following graph shows that when the slope is negative, the value of \theta_1θ1 increases and when it is positive, the value of \theta_1θ1 decreases.

![img](assets/SMSIxKGUEeav5QpTGIv-Pg_ad3404010579ac16068105cfdc8e950a_Screenshot-2016-11-03-00.05.06-20181225144418443.png)

On a side note, we should adjust our parameter \alphaα to ensure that the gradient descent algorithm converges in a reasonable time. Failure to converge or too much time to obtain the minimum value imply that our step size is wrong.

![img](assets/UJpiD6GWEeai9RKvXdDYag_3c3ad6625a2a4ec8456f421a2f4daf2e_Screenshot-2016-11-03-00.05.27-20181225144426639.png)

### How does gradient descent converge with a fixed step size \alphaα?

The intuition behind the convergence is that \frac{d}{d\theta_1} J(\theta_1)dθ1dJ(θ1) approaches 0 as we approach the bottom of our convex function. At the minimum, the derivative will always be 0 and thus we get:

\theta_1:=\theta_1-\alpha * 0θ1:=θ1−α∗0

![img](assets/RDcJ-KGXEeaVChLw2Vaaug_cb782d34d272321e88f202940c36afe9_Screenshot-2016-11-03-00.06.00.png)

\theta_1:=\theta_1-\alpha * 0θ1:=θ1−α∗0