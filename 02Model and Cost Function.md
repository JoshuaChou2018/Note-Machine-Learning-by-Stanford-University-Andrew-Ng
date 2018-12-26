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



