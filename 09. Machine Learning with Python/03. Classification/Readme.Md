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

### K-Nearest Neighbors algorithm
The K-Nearest Neighbors algorithm is a classification algorithm that takes a bunch of labeled points and uses them to learn how to label other points. This algorithm classifies cases based on their similarity to other cases. In K-Nearest Neighbors, data points that are near each other are said to be neighbors. K-Nearest Neighbors is based on this paradigm. Similar cases with the same class labels are near each other. Thus, the distance between two cases is a measure of their dissimilarity. There are different ways to calculate the similarity or conversely, the distance or dissimilarity of two data points. For example, this can be done using Euclidean distance. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/e92d7119-a083-41eb-b944-24d252c3623a.png" width="400" />

In a classification problem, the K-Nearest Neighbors algorithm works as follows: 
1. Pick a value for K 
2. Calculate the distance from the new case, hold out from each of the cases in the dataset
3. Search for the K-observations in the training data that are 'nearest' to the measurements of the unknown data point 
4. Predict the response of the unknown data point using the most popular response value from the K-Nearest Neighbors

There are 2 parts in this algorithm that might be confusing: 
1. How to select the correct K?
2. How to compute the similarity between cases e.g., among customers?

#### Start with second concern: how can we calculate the similarity between two data points? 
Assume that we have two customers, customer one and customer two, and for a moment, assume that these two customers have only one feature, H. We can easily use a specific type of Minkowski distance to calculate the distance of these two customers, it is indeed the Euclidean distance. Distance of X_1 from X_2 is root of 34 minus 30 to power of two, which is four. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/c76ce80b-1047-436e-80c9-2949fc6e94f7.png" width="400" />

What about if we have more than one feature? For example, age and income. If we have income and age for each customer, we can still use the same formula but this time, we're using it in a two dimensional space. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/aabce727-0d87-419f-bb25-cdf1b82fb213.png" width="400" />

We can also use the same distance matrix for multidimensional vectors. Of course, we have to normalize our feature set to get the accurate dissimilarity measure. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/f0436028-03d6-476f-bbd4-a0a7f2ac9d15.png" width="400" />

There are other dissimilarity measures as well that can be used for this purpose but it is highly dependent on datatype and also the domain that classification is done for it. 

#### How to select the correct K?
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

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/5f91cc5f-8d94-4794-b739-2dd05d3a22ad.png" width="400" />

Another way of looking at accuracy of classifiers is to look at a confusion matrix. For example, let’s assume that our test set has only 40 rows. This matrix shows the corrected and wrong predictions, in comparison with the actual labels. Each confusion matrix row shows the Actual/True labels in the test set, and the columns show the predicted labels by classifier. 

let's Look at the first row. The first row is for customers whose actual churn value in the test set is 1. As you can calculate, out of 40 customers, the churn value of 15 of them is 1. And out of these 15, the classifier correctly predicted 6 of them as 1, and 9 of them as 0. This means that for 6 customers, the actual churn value was 1, in the test set, and the classifier also correctly predicted those as 1. However, while the actual label of 9 customers was 1, the classifier predicted those as 0, which is not very good. We can consider this as an error of the model for the first row. What about the customers with a churn value 0? Let’s look at the second row. It looks like there were 25 customers whose churn value was 0. The classifier correctly predicted 24 of them as 0, and one of them wrongly predicted as 1. So, it has done a good job in predicting the customers with a churn value of 0. A good thing about the confusion matrix is that it shows the model’s ability to correctly predict or separate the classes. In the specific case of a binary classifier, such as this example, we can interpret these numbers as the count of true positives, false negatives, true negatives, and false positives. Based on the count of each section, we can calculate the precision and recall of each label. Precision is a measure of the accuracy, provided that a class label has been predicted. It is defined by: precision = True Positive / (True Positive + False Positive). And Recall is the true positive rate. It is defined as: Recall = True Positive / (True Positive + False Negative). So, we can calculate the precision and recall of each class. 

#### F1-score
Now we’re in the position to calculate the F1 scores for each label, based on the precision and recall of that label. 

The F1 score is the harmonic average of the precision and recall, where an F1 score reaches its best value at 1 (which represents perfect precision and recall) and its worst at 0. It is a good way to show that a classifier has a good value for both recall and precision. It is defined using the F1-score equation. For example, the F1-score for class 0 (i.e. churn=0), is 0.83, and the F1-score for class 1 (i.e. churn=1), is 0.55. And finally, we can tell the average accuracy for this classifier is the average of the F1-score for both labels, which is 0.72 in our case. Please notice that both Jaccard and F1-score can be used for multi-class classifiers as well, which is out of scope for this course. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/43b6bb70-4a1b-4d0b-bc1c-37ed55d49c88.png" width="400" />

#### Log loss
Now let's look at another accuracy metric for classifiers. Sometimes, the output of a classifier is the probability of a class label, instead of the label. For example, in logistic regression, the output can be the probability of customer churn, i.e., yes (or equals to 1). This probability is a value between 0 and 1. Logarithmic loss (also known as Log loss) measures the performance of a classifier where the predicted output is a probability value between 0 and 1. So, for example, predicting a probability of 0.13 when the actual label is 1, would be bad and would result in a high log loss. We can calculate the log loss for each row using the log loss equation, which measures how far each prediction is, from the actual label. Then, we calculate the average log loss across all rows of the test set. It is obvious that ideal classifiers have progressively smaller values of log loss. So, the classifier with lower log loss has better accuracy. 

<img src="https://github.com/mauritsvzb/IBM-Data-Science-Professional-Certificate/assets/13508894/2580a43d-adc1-4404-adab-98b16f0754fa.png" width="400" />
