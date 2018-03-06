# Predict quality of the connection

In this lab we will try to build a network intrusion detector, a predictive model capable of distinguishing between bad connections, called intrusions or attacks, and good normal connections.

## Data
Today we are using data set from UCI.This dataset was used for The Third International Knowledge Discovery and Data Mining Tools Competition, which was held in conjunction with KDD-99 The Fifth International Conference on Knowledge Discovery and Data Mining. This dataset contains a standard set of data to be audited, which includes a wide variety of intrusions simulated in a military network environment.


## Create Notebook from link
1. Click on new notebook link on assets page of your project.
![new notebook](https://github.com/IBMDataScience/Strata2018/blob/master/Jupyter%20Notebook/images/new%20notebook.png)

2. Copy path of notebook from github.

3. Select *From URL* option to create notebook. Give name to the notebook and paste url copied from github under *Notebook URL* section.
4. Select box for environment feature and select Default Anaconda XS environment and hit *Create Notebook* button.
![new notebook from url](https://github.com/IBMDataScience/Strata2018/blob/master/Jupyter%20Notebook/images/cretae%20notebook%20from%20url.png)

## Data
 Today we are using KDD Cup 1999  dataset from UCI repository.
 This dataset was used for The Third International Knowledge Discovery and Data Mining Tools Competition, which was held in conjunction with KDD-99 The Fifth International Conference on Knowledge Discovery and Data Mining. This dataset contains a standard set of data to be audited, which includes a wide variety of intrusions simulated in a military network environment.

## Preprocessing
1. Assign column names to the data frame
2. Clean values by removing '.' from label columns
3. Encode normal connection as 1 and all other connections as 0. These are bad connections.
4. Create dummies for categorical variables.
5. Downsample data to 100000 records.

## Train - Test Splitting
Divide data into train and test data sets.

##  Build Parallel XGBoost Classifier

First lets try multithreading with default environment. We can see that there is no improvement in the speed after 2 threads because with XS environment we have only 2 cpus. Now lets upgrade environment to Small and see if we can make any improvement.

## Switch Environment to Default Anaconda S
Change environment to anaconda s (small) and again run the code.

![Change Environment](https://github.com/IBMDataScience/Strata2018/blob/master/Jupyter%20Notebook/images/change%20environment.png)

Now we can see there is improvement in the time taken to train the XG Boost model.

![Parallel model results](https://github.com/IBMDataScience/Strata2018/blob/master/Jupyter%20Notebook/images/XGBoost%20multithreding%20results.png)

## Predict

Now let's make predictions on the test data set.

## Deploy model
In this section we will store  model in Watson Machine Learning repository by using common python client.
To deploy the model  we'll need our Watson Machine Learning credentials. We're going to use the Watson Machine Learning Client for python to save an XGBoost model to our repository. From there, we can bring this model in DSX Projects, take advantage of API endpoints, track development with version control, and much more. Read more in the documentation
[documentation](http://wml-api-pyclient.mybluemix.net)
