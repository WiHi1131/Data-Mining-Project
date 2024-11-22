___

# Section 1

**File:** `Will-K-Means.ipynb`

**Goal**: Generate clusers using K-Means for data in `primary.csv`.

**Reason**: After our Data Exploration phase and visualizing correlations (or the lack thereof) with different numerical variables revealed that it might be difficult to find any strong explanatory variables from our scraped dataset. For this reason, our first step was to generate clusters of data from a K-Means approach, to try and discern whether our dataset contained any identifiable groups with relevant features that would be worth predicting.

## Preprocessing

Before implementing the K-Means model, some processing had to be done on the dataset. Below is a snippet of what the dataset looked like before processing:

![1](milestone-3-visualizations/1.png)

Note that this snippet does not contain all columns of the dataset. 

### Transformation:

Notice the presence of many columns containing long strings or dictionaries of text information. K-Means models can only be conducted with numerical data. Our data contained a column called ‘sentiment’ with string values containing a numerical score along with explanations and other indicators of sentiment, such as numbers of positive/negative words within each article. It was decided that sentiment score might be a useful attribute to try and create clusters from, so the numerical part of this string needed to be separated. This numerical score was first extracted and put into a new column with the following code:  

![2](milestone-3-visualizations/2.png)

After creating this column, all numerical columns were defined and isolated:

![3](milestone-3-visualizations/3.png)

Two significant outliers were also identified, and dropped from the dataset:

![4](milestone-3-visualizations/4.png)

It is standard practice to implement scaling of values for K-Means clustering models, so a StandardScaler from Scikit-learn was also used. Below shows a snippet of the implementation of scaling, and how the scaled data looked before K-Means was performed:

![5](milestone-3-visualizations/5.png)

## Modeling

### K-Means Clustering:

First, we much implement K-Means and select a value for K. Many values of K were tested, and the clusters were visualized in two dimensions using principal component analysis. From visualizations that were only possible from reducing the dimensions to two, a value for K = 3 was chosen. Since the outcome of the k-means clustering was, for us, a somewhat exploratory measure, we believe this makes sense over other potential values of k which could have been chosen based off of other metrics, as we will discuss below.  

A K-means model with 3 clusters divided the data into the following groups:

![6](milestone-3-visualizations/6.png)

Using Principal Component Analysis, the dimensions of each of these groups was reduced to two for visualization purposes:

![7](milestone-3-visualizations/7.png)

The visualizations of these dimension-reduced clusters, with each cluster colored differently, is as follows:

![8](milestone-3-visualizations/8.png)

We can see that most of the data belongs to either Cluster 1 or 2, and these clusters are close to each other when visualized. The most interesting cluster for our analysis is Cluster 0. Though this cluster contains the least amount of data points, and those data points have a large spread, they clearly are distinguished from Clusters 1 and 2, having the highest values of the two principal components.  

We can understand this difference further by looking at means of the attributes of the data in each cluster:  

![9](milestone-3-visualizations/9.png)

We can see that Cluster 0 is characterized by the highest means of investor counts, total funding, the last funding amount (the last two by far), and, interestingly, a lower sentiment score than the other two clusters. We also note the similarity with the year founded and funding count as Cluster 1, and a lower magnitude mosaic change than Cluster 1. This paints the following picture: Cluster 0 appears to contain startups that have been around for 9-10 years, but, in contrast to startups in Cluster 1, have more investors and vastly more amounts of funding (though they have had the same rounds of funding as those startups in Cluster 1), a smaller change in mosaic score than Cluster 1, and a noticeably lower sentiment score than either other cluster. We might expect Cluster 2 to have the lowest numbers of investors and funding numbers, since their mean founding year is much more recent. However, the founding year for startups in Cluster 0 is very close to that of Cluster 1, and yet financial metrics for startups in Cluster 0 are significantly better. The difference in mean sentiment score for Cluster 0 startups is particularly intriguing. It may be that the more successful startups in Cluster 0 simply have more press written about them as opposed to other startups, and more press may contain negative sentiment. This could be a direct implementation of the old maxim: “any press is good press”. In other words, more successful startups may have more negative things written about them, but at least this means they get more media coverage, and this translates to much more funding than other startups.  

With all this in mind, we decided the prediction of many of our subsequent models would be to predict the cluster grouping that was generated from this K-means model. 

In terms of hyperparameter tuning, other values for K were considered but were not used due to being less interpretable for further model building and prediction.  

A graph using the elbow method for finding an optimal value of K was generated for consideration:

![10](milestone-3-visualizations/10.png)

We can see there is not any definitive value of K for which the slope of this curve drastically decreases from one value of K to the next – the decrease in distortion is gradual throughout. The largest decreases in the slope appear to occur between k = 2 and k = 3, and between k = 6 and k = 7.   

A visualization of using k = 7 with PCA to reduce dimensions to 2 is as follows:

![11](milestone-3-visualizations/11.png)

We can see a huge amount of variability within the large ball of data that was previously only divided into 2 clusters for K = 3, and the former cluster for Cluster 0 at K = 3 is also divided, with brown points of Cluster 5 being mixed in to the red points of Cluster 3 in the above graph.  

## Conclusion

Though it may be interesting to use such a clustering in a further analysis beyond the scope of this project, it was decided that it would be sufficient to use K = 3 and attempt to find ways to predict any data found to be in Cluster 0, as this appears to have enough interesting differences (from the examination of the means of attributes for data in that cluster) to make predictive models focusing mostly on finding startups that fit into this cluster. 

___

# Section 2

**File:** `Will_DM_NN.ipynb`

**Goal**: Use neural network to predict clusters found with K-Means for data in `primary.csv`. 

**Reason**: After creating the clusters, we created a neural network to make predictions of which companies belong to which clusters. This network looks at numerical features when making a decision.

## Preprocessing

A new dataset was created after K-Means clustering was performed, including the cluster of each datapoint. The below image is a snippet of that data:  

![12](milestone-3-visualizations/12.png)

Note the cluster column on the right-hand side, showing the cluster each data point belongs to.

### Transformation:

Like before, and to keep the model consistent, we used only numerical columns for the neural network:  

![13](milestone-3-visualizations/13.png)

We split the data into training and testing sets, and, like before, used standard scaling, as this is generally best practice for training neural networks: 

![14](milestone-3-visualizations/14.png)

Below is a snippet of how the training data looked before the neural network model was trained on it:  

![15](milestone-3-visualizations/15.png)

## Modeling

### Neural Network:

A very basic and straightforward neural network model with two hidden layers and an output layer was created using the Keras library, which runs on top of TensorFlow, another python library. This was used as a classifier to predict the three classes corresponding to the three k-means clusters we found previously. We decided to use a standard ReLU activation function for hidden layers and a softmax function for the output layer, because these are suitable for basic classification models such as this. 

![16](milestone-3-visualizations/16.png)

We omitted more complex techniques such as regularization, dropout, or batch normalization, since this was meant to be a baseline model that could potentially be optimized later. The architecture of the model is simple, with only three layers: one hidden ReLU layer with 64 neurons, another hidden ReLU layer with 32 neurons, and an output layer with softmax activation with 3 neurons, suitable for classification. The optimizer (Adam) and loss function (sparse categorical cross-entropy) are both commonly used. The sparse categorical cross entropy function is able to be used here since the labels for the clusters are provided as integers.

![17](milestone-3-visualizations/17.png)

We monitored accuracy during training and evaluation. Nine epochs were chosen after initially trying 30 and noticing an area where the loss function ceased to decrease around nine epochs. Note the training data was also split into a 0.1 size validation set to help prevent overfitting. Overall, this model was created to be extremely basic and as a baseline for further optimization if deemed necessary. Below is the code used, the output of each epoch, and a confusion matrix to evaluate performance:  

![18](milestone-3-visualizations/18.png)

Surprisingly, we saw an extremely high rate of accuracy of prediction even though no class balancing was performed on the data and despite the simplistic nature of the neural network. Note the final accuracy on the test set was 0.9873. We can also examine the confusion matrix above. We can see the only errors are 6 predictions that an item would be in class 0, but was actually in class 1, 7 items predicted to be in class 2, but were actually in class 1, and only 1 item predicted to be in class 0, but was actually in class 2. Since Class 0 is our interesting class and the one that would likely yield startups most likely to receive large amounts of funding, we likely don’t care much about incorrect predictions of class 2 items that were actually in class 1. We do see that this neural network tends to place some items in class 0 that do not belong there – considering the rarity of a startup actually belonging to class 0, this may be a bit concerning should this model be introduced to new data (7 wrong predictions out of 45 predicted to be in Class 0 would give us a 15% likelihood that our model might tell us to invest in a Class 0 company that is not actually classified as one). Of course, since we are predicting clusters and not actual performance of a company, it is entirely possible that a Class 1 or 2 company might contain some metrics like funding amount that would be favorable, even if they are not within our ‘interesting’ cluster. And, regardless, an 85% accurate prediction for Class 0 is still very good considering how imbalanced the classes are in this case.  

## Conclusion

Our model performs extremely well without the need for class balancing or adjustment of a very simple neural network. With such an excellent accuracy score, we should be wary of possible overfitting. The best way to uncover overfitting would be to find out how well this model performs on brand-new, unseen data. 






<a href="https://wihi1131.github.io/Data-Mining-Project/">Home</a>





