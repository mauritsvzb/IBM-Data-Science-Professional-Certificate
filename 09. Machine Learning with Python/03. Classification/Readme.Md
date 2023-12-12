# Classification
## Definition
In machine learning, classification is a supervised learning approach which can be thought of as a means of categorizing or classifying some unknown items into a discrete set of classes. Classification attempts to learn the relationship between a set of feature variables and a target variable of interest. The target attribute in classification is a categorical variable with discrete values. Given a set of training data points along with the target labels, classification determines the class label for an unlabeled test case.

## Use Cases
### Binary Classification
A good example of classification is the loan default prediction. Suppose a bank is concerned about the potential for loans not to be repaid. If previous loan default data can be used to predict which customers are likely to have problems repaying loans, these bad risk customers can either have their loan application declined or offered alternative products. The goal of a loan default predictor is to use existing loan default data which has information about the customers such as age, income, education, etc., to build a classifier, pass a new customer or potential future default to the model, and then label it, i.e the data points as defaulter or not defaulter. This is how a classifier predicts an unlabeled test case. Note that this specific example is a a binary classifier with two values.

### Multi-Class Classification
Classifier models can be built for both binary classification and multi-class classification. For example, imagine that you've collected data about a set of patients, all of whom suffered from the same illness. During their course of treatment, each patient responded to one of three medications. You can use this labeled dataset with a classification algorithm to build a classification model. Then you can use it to find out which drug might be appropriate for a future patient with the same illness.

### Churn Detection and Other Applications
Classification can also be used to predict the category to which a customer belongs, for churn detection where we predict whether a customer switches to another provider or brand, or to predict whether or not a customer responds to a particular advertising campaign. Data classification has several applications in a wide variety of industries. Essentially, many problems can be expressed as associations between feature and target variables, especially when labelled data is available. This provides a broad range of applicability for classification. For example, classification can be used for email filtering, speech recognition, handwriting recognition, biometric identification, document classification and much more.

## Module Scope
This module will consider some of the many types of classification algorithms, such as 
* k-nearest neighbor (KNN)
* decision trees 
* logistic regression
* support vector machines (SVM)

There are many more types of classification algorithms.

## K-Nearest Neighbors algorithm
The K-Nearest Neighbors algorithm is a classification algorithm that takes a bunch of labeled points and uses them to learn how to label other points. This algorithm classifies cases based on their similarity to other cases. In K-Nearest Neighbors, data points that are near each other are said to be neighbors. K-Nearest Neighbors is based on this paradigm. Similar cases with the same class labels are near each other. Thus, the distance between two cases is a measure of their dissimilarity. There are different ways to calculate the similarity or conversely, the distance or dissimilarity of two data points. For example, this can be done using Euclidean distance. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/e92d7119-a083-41eb-b944-24d252c3623a.png" width="400" />

In a classification problem, the K-Nearest Neighbors algorithm works as follows: 
1. Pick a value for K 
2. Calculate the distance from the new case, hold out from each of the cases in the dataset
3. Search for the K-observations in the training data that are 'nearest' to the measurements of the unknown data point 
4. Predict the response of the unknown data point using the most popular response value from the K-Nearest Neighbors

There are 2 parts in this algorithm: 
1. How to select the correct K?
2. How to compute the similarity between cases e.g., among customers?

### Start with second concern: how can we calculate the similarity between two data points? 
Assume that we have two customers, customer one and customer two, and for a moment, assume that these two customers have only one feature, H. We can easily use a specific type of Minkowski distance to calculate the distance of these two customers, it is indeed the Euclidean distance. Distance of X_1 from X_2 is root of 34 minus 30 to power of two, which is four. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/c76ce80b-1047-436e-80c9-2949fc6e94f7.png" width="400" />

What about if we have more than one feature? For example, age and income. If we have income and age for each customer, we can still use the same formula but this time, we're using it in a two dimensional space. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/aabce727-0d87-419f-bb25-cdf1b82fb213.png" width="400" />

We can also use the same distance matrix for multidimensional vectors. Of course, we have to normalize our feature set to get the accurate dissimilarity measure. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/f0436028-03d6-476f-bbd4-a0a7f2ac9d15.png" width="400" />

There are other dissimilarity measures as well that can be used for this purpose but it is highly dependent on datatype and also the domain that classification is done for it. 

### How to select the correct K?
Assume that we want to find the class of the customer noted as question mark on the chart. What happens if we choose a very low value of K? Let's say, K equals one. The first nearest point would be blue, which is class one. This would be a bad prediction, since more of the points around it are magenta or class four. In fact, since its nearest neighbor is blue we can say that we capture the noise in the data or we chose one of the points that was an anomaly in the data. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/b0989e08-167f-4dd3-9b0e-27cb54e82bde.png" width="400" />

A low value of K causes a highly complex model as well, which might result in overfitting of the model. It means the prediction process is not generalized enough to be used for out-of-sample cases. Out-of-sample data is data that is outside of the data set used to train the model. In other words, it cannot be trusted to be used for prediction of unknown samples. It's important to remember that overfitting is bad, as we want a general model that works for any data, not just the data used for training. Now, on the opposite side of the spectrum, if we choose a very high value of K such as K equals 20, then the model becomes overly generalized. So, how can we find the best value for K? The general solution is to reserve a part of your data for testing the accuracy of the model. Once you've done so, choose K equals one and then use the training part for modeling and calculate the accuracy of prediction using all samples in your test set. Repeat this process increasing the K and see which K is best for your model. For example, in our case, K equals four will give us the best accuracy. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/d6eb3422-849c-4386-b5ae-1e37fa890352.png" width="400" />

Nearest neighbors analysis can also be used to compute values for a continuous target. In this situation, the average or median target value of the nearest neighbors is used to obtain the predicted value for the new case. For example, assume that you are predicting the price of a home based on its feature set, such as number of rooms, square footage, the year it was built, and so on. You can easily find the three nearest neighbor houses not only based on distance but also based on all the attributes and then predict the price of the house as the medium of neighbors.

### Evaluation Metrics in Classification

Evaluation metrics explain the performance of a model. Evaluation metrics provide a key role in the development of a model, as they provide insight to areas that might require improvement. There are different model evaluation metrics but we just talk about three of them here, specifically: 
* Jaccard index
* F1-score 
* Log Loss 

#### Jaccard index (aka Jaccard similarity coefficient)
Let’s say y shows the true labels of the churn dataset. And y ̂ shows the predicted values by our classifier. Then we can define Jaccard as the size of the intersection divided by the size of the union of two label sets (i.e., total sample size - size of intersection). For example, for a test set of size 10, with 8 correct predictions, or 8 intersections, the accuracy by the Jaccard index would be 0.66. If the entire set of predicted labels for a sample strictly matches with the true set of labels, then the subset accuracy is 1.0; otherwise it is 0.0. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/5f91cc5f-8d94-4794-b739-2dd05d3a22ad.png" width="600" />

Another way of looking at accuracy of classifiers is to look at a confusion matrix. For example, let’s assume that our test set has only 40 rows. This matrix shows the corrected and wrong predictions, in comparison with the actual labels. Each confusion matrix row shows the Actual/True labels in the test set, and the columns show the predicted labels by classifier. 

Let's look at the first row. The first row is for customers whose actual churn value in the test set is 1. As you can calculate, out of 40 customers, the churn value of 15 of them is 1. And out of these 15, the classifier correctly predicted 6 of them as 1, and 9 of them as 0. This means that for 6 customers, the actual churn value was 1, in the test set, and the classifier also correctly predicted those as 1. However, while the actual label of 9 customers was 1, the classifier predicted those as 0, which is not very good. We can consider this as an error of the model for the first row. What about the customers with a churn value 0? Let’s look at the second row. It looks like there were 25 customers whose churn value was 0. The classifier correctly predicted 24 of them as 0, and one of them wrongly predicted as 1. So, it has done a good job in predicting the customers with a churn value of 0. A good thing about the confusion matrix is that it shows the model’s ability to correctly predict or separate the classes. In the specific case of a binary classifier, such as this example, we can interpret these numbers as the count of true positives, false negatives, true negatives, and false positives. Based on the count of each section, we can calculate the precision and recall of each label. Precision is a measure of the accuracy, provided that a class label has been predicted. It is defined by: precision = True Positive / (True Positive + False Positive). And Recall is the true positive rate. It is defined as: Recall = True Positive / (True Positive + False Negative). So, we can calculate the precision and recall of each class. 

#### F1-score
Now we’re in the position to calculate the F1 scores for each label, based on the precision and recall of that label. 

The F1 score is the harmonic average of the precision and recall, where an F1 score reaches its best value at 1 (which represents perfect precision and recall) and its worst at 0. It is a good way to show that a classifier has a good value for both recall and precision. It is defined using the F1-score equation. For example, the F1-score for class 0 (i.e. churn=0), is 0.83, and the F1-score for class 1 (i.e. churn=1), is 0.55. And finally, we can tell the average accuracy for this classifier is the average of the F1-score for both labels, which is 0.72 in our case. Please notice that both Jaccard and F1-score can be used for multi-class classifiers as well. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/43b6bb70-4a1b-4d0b-bc1c-37ed55d49c88.png" width="600" />

#### Log loss
Sometimes, the output of a classifier is the probability of a class label, instead of the label. For example, in logistic regression, the output can be the probability of customer churn, i.e., yes (or equals to 1). This probability is a value between 0 and 1. Logarithmic loss (also known as Log loss) measures the performance of a classifier where the predicted output is a probability value between 0 and 1. So, for example, predicting a probability of 0.13 when the actual label is 1, would be bad and would result in a high log loss. We can calculate the log loss for each row using the log loss equation, which measures how far each prediction is, from the actual label. Then, we calculate the average log loss across all rows of the test set. It is obvious that ideal classifiers have progressively smaller values of log loss. So, the classifier with lower log loss has better accuracy. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/2580a43d-adc1-4404-adab-98b16f0754fa.png" width="600" />

## Decision Trees
Imagine that you're a medical researcher compiling data for a study. You've already collected data about a set of patients all of whom suffered from the same illness. During their course of treatment, each patient responded to one of two medications. We call them drug A and drug B. Part of your job is to build a model to find out which drug might be appropriate for a future patient with the same illness. The feature sets of this dataset are age, gender, blood pressure, and cholesterol of our group of patients and the target is the drug that each patient responded to. It is a sample of binary classifiers, and you can use the training part of the data set to build a decision tree and then use it to predict the class of an unknown patient. In essence, to come up with a decision on which drug to prescribe to a new patient. Let's see how a decision tree is built for this dataset. 

Decision trees are built by splitting the training set into distinct nodes, where one node contains all of or most of one category of the data. If we look at the diagram here, we can see that it's a patient's classifier. So as mentioned, we want to prescribe a drug to a new patient, but the decision to choose drug A or B will be influenced by the patient's situation. We start with age, which can be young, middle aged or senior. If the patient is middle aged, then we'll definitely go for drug B. On the other hand, if he has a young or a senior patient, will need more details to help us determine which drug to prescribe. The additional decision variables can be things such as cholesterol levels, gender or blood pressure. For example, if the patient is female, then we will recommend drug A, but if the patient is male, then will go for drug B. As you can see, decision trees are about testing an attribute and branching the cases based on the result of the test. Each internal node corresponds to a test, and each branch corresponds to a result of the test, and each leaf node assigns a patient to a class. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/9b853c12-4461-42a2-b15d-e215601129d8.png" width="600" />

How to build such a decision tree? A decision tree can be constructed by considering the attributes one by one. 
1. Choose an attribute from the dataset
2. Calculate the significance of the attribute in the splitting of the data
3. split the data based on the value of the best attribute
4. Repeat steps 1-3 for remaining attributes

After building this tree, you can use it to predict the class of unknown cases; or in our case, the proper drug for a new patient based on his or her characteristics

### Building Decision Trees
Decision trees are built using recursive partitioning to classify the data. Let's say we have 14 patients in our data set, the algorithm chooses the most predictive feature to split the data on. What is important in making a decision tree, is to determine which attribute is the best or more predictive to split data based on the feature. Let's say we pick cholesterol as the first attribute to split data, it will split our data into two branches. As you can see, if the patient has high cholesterol we cannot say with high confidence that drug B might be suitable for him. Also, if the patient's cholesterol is normal, we still don't have sufficient evidence or information to determine if either drug A or drug B is in fact suitable. It is a sample of bad attributes selection for splitting data. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/5f05ef0b-f266-4c9b-9d37-d6592ccfb8e4.png" width="600" />

So, let's try another attribute. Again, we have our 14 cases, this time we picked the sex attribute of patients. It will split our data into two branches, male and female. As you can see, if the patient is female, we can say drug B might be suitable for her with high certainty. But if the patient is male, we don't have sufficient evidence or information to determine if drug A or drug B is suitable. However, it is still a better choice in comparison with the cholesterol attribute because the result in the nodes are more pure. It means nodes that are either mostly drug A or drug B. So, we can say the sex attribute is more significant than cholesterol, or in other words it's more predictive than the other attributes. Indeed, predictiveness is based on decrease in impurity of nodes. We're looking for the best feature to decrease the impurity of patients in the leaves, after splitting them up based on that feature. So, the sex feature is a good candidate in the following case because it almost found the pure patients. Let's go one step further. For the male patient branch, we again test other attributes to split the sub-tree. We test cholesterol again here, as you can see it results in even more pure leaves. So we can easily make a decision here. For example, if a patient is male and his cholesterol is high, we can certainly prescribe drug A, but if it is normal, we can prescribe drug B with high confidence. As you might notice, the choice of attribute to split data is very important and it is all about purity of the leaves after the split. A node in the tree is considered pure if in 100 percent of the cases, the nodes fall into a specific category of the target field. In fact, the method uses recursive partitioning to split the training records into segments by minimizing the impurity at each step. Impurity of nodes is calculated by entropy of data in the node. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/f46aee46-bf68-4f6e-a55d-0882204b6254.png" width="600" />

So, what is entropy? Entropy is the amount of information disorder or the amount of randomness in the data. The entropy in the node depends on how much random data is in that node and is calculated for each node. In decision trees, we're looking for trees that have the smallest entropy in their nodes. The entropy is used to calculate the homogeneity of the samples in that node. If the samples are completely homogeneous, the entropy is zero and if the samples are equally divided it has an entropy of one. This means if all the data in a node are either drug A or drug B, then the entropy is zero, but if half of the data are drug A and other half are B then the entropy is one. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/2a0d9f14-d73e-4cc8-870d-66501d6878b4.png" width="600" />

You can easily calculate the entropy of a node using the frequency table of the attribute through the entropy formula where P is for the proportion or ratio of a category, such as drug A or B. Please remember though that you don't have to calculate these as it's easily calculated by the libraries or packages that you use. As an example, let's calculate the entropy of the data set before splitting it. We have nine occurrences of drug B and five of drug A. You can embed these numbers into the entropy formula to calculate the impurity of the target attribute before splitting it. In this case, it is 0.94. So, what is entropy after splitting? Now, we can test different attributes to find the one with the most predictiveness, which results in two more pure branches. Let's first select the cholesterol of the patient and see how the data gets split based on its values. For example, when it is normal we have six for drug B, and two for drug A. We can calculate the entropy of this node based on the distribution of drug A and B which is 0.8 in this case. But, when cholesterol is high, the data is split into three for drug B and three for drug A. Calculating it's entropy, we can see it would be 1.0. We should go through all the attributes and calculate the entropy after the split and then choose the best attribute. Okay. Let's try another field. Let's choose the sex attribute for the next check. As you can see, when we use the sex attribute to split the data, when its value is female, we have three patients that responded to drug B and four patients that responded to drug A. The entropy for this node is 0.98 which is not very promising. However, on the other side of the branch, when the value of the sex attribute is male, the result is more pure with sex for drug B and only one for drug A. The entropy for this group is 0.59. 

Now, the question is between the cholesterol and sex attributes which one is a better choice? Which one is better at the first attribute to divide the data-set into two branches? Or in other words, which attribute results in more pure nodes for our drugs? Or in which tree do we have less entropy after splitting rather than before splitting? The sex attribute with entropy of 0.98 and 0.59 or the cholesterol attribute with entropy of 0.81 and 1.0 in it's branches. The answer is the tree with the higher information gain after splitting. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/13e8ff8a-69de-4ec5-be6f-bf0e3068b32e.png" width="600" />

So, what is information gain? Information gain is the information that can increase the level of certainty after splitting. It is the entropy of a tree before the split minus the weighted entropy after the split by an attribute. We can think of information gain and entropy as opposites. As entropy or the amount of randomness decreases, the information gain or amount of certainty increases and vice versa. So, constructing a decision tree is all about finding attributes that return the highest information gain. Let's see how information gain is calculated for the sex attribute. As mentioned, the information gained is the entropy of the tree before the split minus the weighted entropy after the split. The entropy of the tree before the split is 0.94, the portion of female patients is seven out of 14 and its entropy is 0.985. Also, the portion of men is seven out of 14 and the entropy of the male node is 0.592. The result of a square bracket here is the weighted entropy after the split. So, the information gain of the tree if we use the sex attribute to split the data set is 0.151. As you could see, we will consider the entropy over the distribution of samples falling under each leaf node and we'll take a weighted average of that entropy weighted by the proportion of samples falling under that leave. We can calculate the information gain of the tree if we use cholesterol as well. It is 0.48. Now, the question is, which attribute is more suitable? Well, as mentioned, the tree with the higher information gained after splitting, this means the sex attribute. So, we select the sex attribute as the first splitter. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/9c3d81f4-7f2b-492b-a398-c221ebefd25b.png" width="600" />

Now, what is the next attribute after branching by the sex attribute? Well, as you can guess, we should repeat the process for each branch and test each of the other attributes to continue to reach the most pure leaves. 

## Logistic Regression (classification context)
We'll address 3 questions:
1. What is logistic regression?
2. What kind of problems can be solved by logistic regression?
3. In which situations do we use logistic regression?

### What is logistic regression

Logistic regression is a statistical and machine learning technique for classifying records (binary or multiclass classification) of a dataset based on the values of the input fields. In logistic regression, independent variables should be continuous. If categorical, they should be dummy or indicator coded. 

### Applications of logistic regression to predict:
* The probability of a person having a heart attack within a specified time period (based on our knowledge of the person's age, sex, and body mass index)
* The chance of mortality in an injured patient
* Whether a patient has a given disease (such as diabetes based on observed characteristics of that patient such as weight, height, blood pressure, and results of various blood tests etc) 
* In a marketing context, the likelihood of a customer purchasing a product or halting a subscription (as we've done in our churn example)
* The probability of failure of a given process, system or product
* The likelihood of a homeowner defaulting on a mortgage. 
Notice that in all these examples not only do we predict the class of each case, we also measure the probability of a case belonging to a specific class. 

### When is logistic regression suitable?
* When the target field in your data is categorical, or specifically, is binary 
  * zero/one, yes/no, churn or no churn, positive/negative etc
* If you need the probabilistic results (linear regression provides predicted outcomes, but not their probabilities)
* If your data is linearly separable

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/f0492a07-6bd0-4327-b808-e8c669f7e3e0.png" width="300" />

* If you need to understand the impact of a feature
  * You can select the best features based on the statistical significance of the logistic regression model coefficients or parameters. That is, after finding the optimum parameters, a feature X with the weight Theta1 close to zero has a smaller effect on the prediction than features with large absolute values of Theta1. Indeed, it allows us to understand the impact an independent variable has on the dependent variable while controlling other independent variables. 

## Suppport Vector Machines (SVM)
A Support Vector Machine is a supervised algorithm that classifies cases by finding a separator. 
1. Map data to a high dimensional feature space 
2. Estimate a Non-Linear Separator (drawn as hyperplane)

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/a5c527ce-06d6-4348-86dd-aadb59755c9e.png" width="300" /> <img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/d3333205-fa94-46fc-b502-e42b33d58aa5.png" width="300" />

Two challenging questions to consider: 
1. How do we transfer data in such a way that a separator could be drawn as a hyperplane? 
2. How can we find the best or optimized hyperplane separator after transformation? 

### Data transformation
Kernelling in SVM is the transforming/mapping of data into higher dimensional space, in such a way that can change a linearly inseparable data set into a linearly separable data set. The mathematical function used for the transformation is known as the kernel function, and can be of different types:
* Linear
* Polynomial
* Radial Basis Function (RBF)
* Sigmoid

Each of these functions has its own characteristics, its pros and cons, and its own equation, and can be implemented in libraries of different DS languages. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/c737671c-08df-4041-a17b-b8a15445db70.png" width="300" />

There's no easy way of knowing which function performs best with any given dataset. Choose different functions in turn and compare the results. 

### How do we find the right or optimized hyperplane separator after transformation? 
SVMs are based on the idea of finding a hyperplane that best divides a data set into two classes. One reasonable choice as the best hyperplane is the one that represents the largest separation or margin between the two classes. So the goal is to choose a hyperplane with as big a margin as possible. Examples closest to the hyperplane are support vectors. It is intuitive that only support vectors matter for achieving our goal. And thus, other trending examples can be ignored. We tried to find the hyperplane in such a way that it has the maximum distance to support vectors. Please note that the hyperplane and boundary decision lines have their own equations. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/e698f108-dd7c-4452-aa69-cb2a8272b11d.png" width="300" />

The hyperplane is learned from training data using an optimization procedure that maximizes the margin. The outputs of the algorithm are the values w and b for the line. You can make classifications using this estimated line. It is enough to plug in input values into the line equation. Then, you can calculate whether an unknown point is above or below the line. 
* If the equation returns a value greater than 0, then the point belongs to the first class which is above the line
* If the equation returns a value smaller than 0, then the point belongs to the second class which is below the line

### Pros and Cons of SVM
* Pros
 * Accurate in high-dimensional spaces
 * Memory efficient

* Cons
 * Prone to overfitting
 * No probability estimation
 * Small data sets

### SVM applications
* Image classification
* Text category assignment 
* Detecting spam
* Sentiment analysis
* Gene expression classification
* Regression, outlier detection, and clustering
