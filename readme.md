1.Overview
After data preparation was done, we already get the dataset which contains essential information about value of each song’s attribute. So, what we next to do is applying KNN algorithm in this dataset and building the model in order to classify each genre of music. The principle is that different types of music have different performances in different attributes. For instance, as picture shows below, the classical music usually has low level of energy and low level of ‘speechiness’, which are absolutely opposed to pop music. Meanwhile, the classical music often takes instruments in playing, so, the instrumental value ‘instrumentalness’ of classical music is higher than ‘instrumentalness’ value of pop music. After we building model using historical dataset, we finally could get the feature model of different types of music. Combined with the plug-ins designed for different types of music, when the new song is put into the Spotify’s music library, the system will match the similar types of songs for the new song according to the model algorithm, and design plug-ins for the new songs according to the plug-ins used in similar song.

2.Introduction for KNN
KNN, which full name is k-nearest neighbor, is one of the simplest methods in data mining classification technology, also is a mature method in theory and one of the simplest machine learning algorithms. The idea of this method is very simple and intuitive: if majority of the k most similar samples of a data point in the feature space (i.e., the nearest samples in the feature space) belong to a certain category, then the data point also belongs to this category. In the decision-making of classification, the method only determines the category of the sample to be classified according to the category of the nearest one or several samples. The advantage for this method is that KNN is simple and easy method to understand, and it easy to implement, and we do not need to estimate parameters. 
3.Procedures
a.Prepare historical data and preprocess the data
b.import historical data, and initially establish the feature space of historical sample points, namely KNN model
c.Using Python package GridSearch, the optimal K value and its corresponding optimal model are screened out based on the model selection standard AUC
d.Use test sample points to check model performance
4.Implementation

At the first, we input data file into python environment. After computer reads file and transforms it into data frame, we need also clean the data, such like drop the missing value of data or fix the irregular data.

Second, we need to drop the useless variables like low-relevance variables or exante predictors. Next, we split variables into numerical variable and categorical variables using ‘float64’ and ‘category’ index. 

In the next step, the numerical variables need to be standardized because we need to reduce numerical influence of data value to our model. The categorical predictors need to be dummied and we also drop the dummies because the categorical variables are informative. In our project, we need to build 5 KNN models. So, we drop five dummies except dummy ‘genre_pop’ in order to build KNN model of Pop music.

Next part is data partition. We split dataset in 2 parts. One is for training model and validation, and another is test part which used in checking model performance. 

Now, we are moving to the most important procedure-training model. First, we introduce package called KNeighborClassifier, it could realize the KNN model in python. Second, we get non-test data prepared, the x which contains predictors except dependent variable and the y which contains only about data of dependent variable are information source for modeling. Then, we introduce in cross-validation function and split data into 5 folds. So, we could train the KNN model of pop music under these 5 folds. Finally, we determine the range of k value, from 1 to 100. So, we could find the optimal K value as well as the best model under this scope. Since different level of K value could generate different model, we chose to select the optimal K value and optimal model for pop music based on AUC performance. It is means that, under the scope of K value, one specific K value which could generate the model with highest AUC performance, is the K value we are looking for. And I would show the optimal K value and corresponding model of other 5 models in result part.

Last movement we need to do is examining optimal K value of KNN model and AUC performance of model. 
5.Result 
We built 6 KNN models for our project, respectively is KNN of pop music, classical music model, Jazz HipHop model, EDM music model, Indie folk model, as well as K-pop model. And AUC performance and optimal K value of each model list below.
KNN MODEL	AUC PERFORMANCE	THE OPTIMAL K
POP	0.8551642142023569	5
CLASSICAL	0.9663015200979391	48
JAZZ HIPHOP	0.9330157198964476	36
EDM	0.8845739785730409	63
INDIE FOLK	0.8721709500578385	49
K-POP	0.9198212065597062	50
6.Conclusion
After we built the models, we could actually apply our model in real situation. The whole procedures of applying model in new data shows as following: First, we input new data in one of our models and count its Euclidean distance with other data in this model. Second, according to the optimal K value of this model and Euclidean distance, the algorithm lists top k data points which have shortest Euclidean distance with new data. Finally, based on majority distribution of type of K data points, we classify the new data. If new data classified as not belong to this model or music type of this model, then apply new data to next model until we find new data’s type. So, we could match the plug-ins for song. 
