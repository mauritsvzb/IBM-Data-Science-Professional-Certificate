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
* k-nearest neighbor (KNN
* decision trees 
* logistic regression
* support vector machines (SVM)

There are many more types of classification algorithms.

### K-Nearest Neighbors algorithm
The K-Nearest Neighbors algorithm is a classification algorithm that takes a bunch of labeled points and uses them to learn how to label other points. This algorithm classifies cases based on their similarity to other cases. In K-Nearest Neighbors, data points that are near each other are said to be neighbors. K-Nearest Neighbors is based on this paradigm. Similar cases with the same class labels are near each other. Thus, the distance between two cases is a measure of their dissimilarity. There are different ways to calculate the similarity or conversely, the distance or dissimilarity of two data points. For example, this can be done using Euclidean distance. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/e92d7119-a083-41eb-b944-24d252c3623a.png" width="400" />

In a classification problem, the K-Nearest Neighbors algorithm works as follows: 
1. Pick a value for K 
2. Calculate the distance from the new case, hold out from each of the cases in the dataset
3. Search for the K-observations in the training data that are 'nearest' to the measurements of the unknown data point 
4. Predict the response of the unknown data point using the most popular response value from the K-Nearest Neighbors

There are 2 parts in this algorithm that might be confusing: 
1. How to select the correct K
2. How to compute the similarity between cases e.g., among customers

#### Start with second concern: how can we calculate the similarity between two data points? 
Assume that we have two customers, customer one and customer two, and for a moment, assume that these two customers have only one feature, H. We can easily use a specific type of Minkowski distance to calculate the distance of these two customers, it is indeed the Euclidean distance. Distance of X_1 from X_2 is root of 34 minus 30 to power of two, which is four. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/c76ce80b-1047-436e-80c9-2949fc6e94f7.png" width="400" />

What about if we have more than one feature? For example, age and income. If we have income and age for each customer, we can still use the same formula but this time, we're using it in a two dimensional space. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/aabce727-0d87-419f-bb25-cdf1b82fb213.png" width="400" />

We can also use the same distance matrix for multidimensional vectors. Of course, we have to normalize our feature set to get the accurate dissimilarity measure. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/f0436028-03d6-476f-bbd4-a0a7f2ac9d15.png" width="400" />

There are other dissimilarity measures as well that can be used for this purpose but as mentioned, it is highly dependent on datatype and also the domain that classification is done for it. 

#### How to select the correct K?
Assume that we want to find the class of the customer noted as question mark on the chart. What happens if we choose a very low value of K? Let's say, K equals one. The first nearest point would be blue, which is class one. This would be a bad prediction, since more of the points around it are magenta or class four. In fact, since its nearest neighbor is blue we can say that we capture the noise in the data or we chose one of the points that was an anomaly in the data. A low value of K causes a highly complex model as well, which might result in overfitting of the model. It means the prediction process is not generalized enough to be used for out-of-sample cases. Out-of-sample data is data that is outside of the data set used to train the model. In other words, it cannot be trusted to be used for prediction of unknown samples. It's important to remember that overfitting is bad, as we want a general model that works for any data, not just the data used for training. Now, on the opposite side of the spectrum, if we choose a very high value of K such as K equals 20, then the model becomes overly generalized. 

So, how can we find the best value for K? The general solution is to reserve a part of your data for testing the accuracy of the model. Once you've done so, choose K equals one and then use the training part for modeling and calculate the accuracy of prediction using all samples in your test set. Repeat this process increasing the K and see which K is best for your model. For example, in our case, K equals four will give us the best accuracy. 

Nearest neighbors analysis can also be used to compute values for a continuous target. In this situation, the average or median target value of the nearest neighbors is used to obtain the predicted value for the new case. For example, assume that you are predicting the price of a home based on its feature set, such as number of rooms, square footage, the year it was built, and so on. You can easily find the three nearest neighbor houses of course not only based on distance but also based on all the attributes and then predict the price of the house as the medium of neighbors.

#### / ### Evaluation Metrics in Classification
