# Predict Chronic Kidney Disease Using SPSS Modeler Flows

## Create Notebook from link
1. Copy path of notebook from github.
2. Click on new notebook link on assets page of your project.
-- Image
3. Select *From URL* option to create notebook.
Give name and paste url copied from githib under *Notebook URL* section.
4. Select box for environment feature and hit *Create Notebook* button.


## Data
 Today we are using KDD Cup 1999  dataset from UCI repository.
 model capable of distinguishing between We will be building predictive model t identify bad connections, called intrusions or attacks, and good or normal connections.

 https://archive.ics.uci.edu/ml/machine-learning-databases/kddcup99-mld/kddcup.data.gz

## Preprocessing
1. Assign column names to the data frame
2. Clean values by removing '.' from label columns
3. Encode normal connection as 1 and all other connections as 0. These are bas connections.
4. Create dummies for categorical variables.
5. Downsample data to 1000000 records.

## Train - Test Splitting
Divide data into train and test data sets.

## Multithreading

First lets try multithreading with default environment. We can see that there is no performance improvement in terms of time taken to train model because we have just 1 cpu in default XS environment.

Change environment to anaconda s (small) and again run the code. Now we can see there is improvement in the time taken to train the XG Boost model.

-- images
