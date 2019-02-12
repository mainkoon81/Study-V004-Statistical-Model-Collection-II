# Probabilistic Graphic Model
 - It's a probabilistic model for which a graph expresses the **conditional dependence structure** between random variables.
   - Let's say we want to classify data points that are independent of each other(for example, given an image, predict whether it contains a cat or a dog), but See `I`, `like`, `machine`, `learning`... Problem here is that `learning` could be a noun or a verb depending on its context. Probabilistic graphical model is a powerful framework which can be used to learn such models with **dependency**.
   - PGM consists of a graph structure. Each `node` of the graph is associated with a random variable, and the `edge` in the graph are used to encode relations between the random variables.
 - Depending on whether the graph is **directed or undirected**, we can classify graphical modes into two categories
   - Bayesian networks
   - Markov networks

### Bayesian Network












---------------------------------------------------------------------------------------------
# Generative VS Discriminative
 - Generative algorithm: learning each structure, and then classifying it using the knowledge you just gained
 - Discriminative algorithm: determining the difference in the each without learning the structure, and then classifying the data_point.
<img src="https://user-images.githubusercontent.com/31917400/52206132-3a894180-2871-11e9-8cdd-81ac93c74e1d.jpg" />

A generative algorithm models how the data was "generated", so you ask it "what's the likelihood this or that class generated this instance?" and pick the one with the **better probability**. A discriminative algorithm uses the data to create a decision boundary, so you ask it "what side of the decision boundary is this instance on?" So it doesn't create a model of how the data was generated, it makes a model of what it thinks the boundary between classes looks like.
 - Estimate joint probability P(Y, X) = P(Y|X)P(X)
 - Estimates not only probability of labels but also the features
 - Once model is fit, can be used to generate data
 - LDA, QDA, Naive Bayes, etc
 - (-) Often works worse, particularly when assumptions are violated

Since **discriminative** cares `P(Y|X)` only, while **generative** cares `P(X,Y) and P(X)` at the same time, in order to predict **P(Y|X)** well, the generative model has **less degree of freedom** in the model compared to discriminative model. So generative model is more robust, less prone to overfitting while discriminative is the other way around. So discriminative models usually tend to do better if you have lots of data; generative models may be better if you have some extra unlabeled data(the generative model has its own advantages such as the capability of dealing with missing data). 
 - Estimate conditional models P(Y|X)
 - Linear regression, Logistic regression




## A> Generative Analysis

 - Rule-based Classification Algorithm:
   - As a **Supervised method**, labels are used to learn the `data structure` which allows the **classification** of future observations.
   - LDA(parametric), QDA
   - KNN
### 1. Linear Discriminant Analysis
# `P(g|x)`
 - Predict the membership of the given vector `x`. 
 - We have a dataset containing lots of vector observations(rows) and their labels. 
 - What's the probability that the new vector observation `x` belongs to the Grp `g`? (p is the dimension of the vector x).
 - This probabilities come from a certain **likelihood distribution of Grp**(with different parametrization)...in detail, 
 <img src="https://user-images.githubusercontent.com/31917400/52278515-2156c280-294f-11e9-9bc2-6e40c4563b8f.jpg" />

 - So let's figure out the Likelihood distribution `P(x|g)`. This is the distribution of data points in each group. If we know the **distribution of x in each Grp: `P(x|g)`**, we can classify the new p-dimensional data points given in the future...so done and dusted. What if choosing the Grp_feature distribution `P(x|g)` as **multivariate Gaussian** ? (Of course, in the multivariate version, `µ` is a mean vector and σ is replaced by a covariance matrix `Σ`).
 <img src="https://user-images.githubusercontent.com/31917400/52270233-3d9b3500-2938-11e9-9585-63ef137328a4.jpg" />

# two functions to maximize `P(g|x)`.
 - Assumption: **all Grp share the equal `Σ` matrix**(in QDA, the equal covariance assumption does not hold, thus you cannot drop `-0.5log(|Σ|)` term).  
 - Which 'g' has the highest probability of owning the new p-dimensional datapoint? 
   - Eventually, Min/Max depends on the unique parameter(`µ,Σ`) of each Grp. 
   - When you plug in x vector, `µ,Σ` that minimizing **Mahalonobis Distance**, is telling you the membership of the vector `x`.  
   <img src="https://user-images.githubusercontent.com/31917400/52273637-57417a00-2942-11e9-8881-f7279ec947d4.jpg" />
   
   - When you plug in x vector, `µ,Σ` that maximizing **LD-function**, is telling you the membership of the vector `x`.
   <img src="https://user-images.githubusercontent.com/31917400/52273639-59a3d400-2942-11e9-900e-077ceabfb0b9.jpg" />
 
 > In practice,
 <img src="https://user-images.githubusercontent.com/31917400/52275738-4dbb1080-2948-11e9-9768-3da4a0c5c773.jpg" />

 > **Log Odd Ratio** and `Linear Decision Boundary`
   - What if the Grp membership probability of 'g1', 'g2' are the same? 
   - Then we can say that the given vector point is the part of `Linear Decision Boundary` !!!
   <img src="https://user-images.githubusercontent.com/31917400/52283578-a2678700-295a-11e9-98ae-817a9f91afdc.jpg" />

 > LDA and Logistic regression
   - LDA is Generative while LogisticRegression is discriminative.
   - LDA operates by maximizing the log-likelihood based on an assumption of normality and homogeneity while Logistic regression makes no assumption about P(X), and estimates the parameters of P(g|x) by maximizing the conditional likelihood. 
   - logistic regression would presumably be more robust if LDA’s distributional assumptions (Gaussian?) are violated. 
   - In principle, LDA should perform poorly when outliers are present, as these usually cause problems when assuming normality. 
   - In LDA, the log-membership odd between Grps are **linear functions** of the vector data x. This is due to the assumption of `Gaussian densities` and `common covariance matrices`.
   - In LogisticRegression, the log-membership odd between Grps are **linear functions** of the vector data x as well. 
   <img src="https://user-images.githubusercontent.com/31917400/52282688-e6f22300-2958-11e9-923a-5be3e22e8de9.jpg" />

### 2. Latent Dirichlet Allocation
 - The finite Dirichlet distribution is a distribution over distributions, namely over multinomial distributions. That means if you draw a sample from it, you get a random distribution. A loaded die can be described by a `multinomial distribution`. A machine that makes biased die with some random error can be described by a `Dirichlet distribution`. Suppose there are boxes with chocolates, with some portion of dark and sweet chocolates. You pick at random one of the boxes(perhaps some kinds of boxes can be more common than others. Then, you can pick at random one of the chocolates. So you have a distribution (a collection of boxes) of distributions (chocolates in a box). 
   - Just as the beta distribution is the conjugate prior for a binomial likelihood, the Dirichlet distribution is the conjugate prior for the multinomial likelihood. It can be thought of as a **multivariate beta distribution** for a collection of probabilities (that must sum to 1). 
 - LDA is a “generative probabilistic model” of a collection of **composites made up of parts**. The composites are `documents` and the parts are `words` in terms of **topic(LatentVariable)** modeling. The probabilistic topic model estimated by LDA consists of two tables (matrices):
   - 1st table: the probability of selecting a particular `part(word)` when sampling a particular **topic(category)**.
   - 2nd table: the probability of selecting a particular **topic(category)** when sampling a particular `document`.
<img src="https://user-images.githubusercontent.com/31917400/52525957-842abf80-2ca9-11e9-8465-b36a9e1d2d4e.jpg" />

 - > In the chart above, every topic is given the same alpha value. Each dot represents some distribution or mixture of the three topics like (1.0, 0.0, 0.0) or (0.4, 0.3, 0.3). Remember that each sample has to add up to one. At low alpha values (less than one), most of the topic distribution samples are in the corners (near the topics). For really low alpha values, it’s likely you’ll end up sampling (1.0, 0.0, 0.0), (0.0, 1.0, 0.0), or (0.0, 0.0, 1.0). This would mean that a document would only ever have one topic if we were building a three topic probabilistic topic model from scratch.
 - > At alpha equal to one, any space on the surface of the triangle (2-simplex) is fair game (uniformly distributed). You could equally likely end up with a sample favoring only one topic, a sample that gives an even mixture of all the topics, or something in between. For alpha values greater than one, the samples start to congregate to the center. This means that as alpha gets bigger, your samples will more likely be uniform or an even mixture of all the topics.
 
 - WTF? __Simplest Generative Procedure:__
   - Pick your unique set of WORDS.
   - Pick how many DOCUMENTS you want.
   - Pick how many WORDS you want per each DOCUMENT (sample from a Poisson distribution).
   - Pick how many `topics`(categories) you want.
   - Pick a number between not zero and positive infinity and call it **alpha**.
   - Pick a number between not zero and positive infinity and call it **beta**.
   - Build the `**WORDS** VS **topics** table`. 
     - For each column, draw a sample(spin the wheel) from a Dirichlet distribution using **beta** as the input. The Dirichlet distribution takes a number called **beta** for each `topic` (or category). 
     - Each sample will fill out each column in the table, sum to one, and give the probability of each part per `topic`(column).
   - Build the `**DOCUMENTS** VS **topics** table`. 
     - For each row, draw a sample from a Dirichlet distribution using **alpha** as the input. The Dirichlet distribution takes a number called alpha for each `topic` (or category).
     - Each sample will fill out each row in the table, sum to one, and give the probability of each `topic` (column) per DOCUMENT.
   - Build the actual DOCUMENTS. For each DOCUMENT:
     - Step_1) look up its **row** in the `**DOCUMENT** VS **topics** table`, 
     - Step_2) sample a `topic` based on the probabilities in the row, 
     - Step_3) go to the `**WORDS** VS **topics** table`, 
     - Step_4) look up the `topic` sampled, 
     - Step_5) sample a **WORD** based on the probabilities in the column, 
     - Step_6) repeat from step 2 until you’ve reached how many WORDS this DOCUMENT was set to have.


### Dirichlet Processes
 - Goal
   - Density Estimation
   - Semi-parametric modelling
   - Sidestepping model selection/averaging
 
 







































































