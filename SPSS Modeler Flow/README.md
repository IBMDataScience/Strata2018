
# Predict Chronic Kidney Disease Using SPSS Modeler Flows

In this lab we will try to predict chronic kidney disease using various attributes collected from hospitals. Chronic kidney disease (CKD) is a condition characterized by a gradual loss of kidney function over time, which may lead to kidney failure.

## Data
We are using the UCI Chronic Kidney Disease data set from the Data Science Experience community. You can get data into your project in two simple steps.

 #### Step 1
 Go to the [Data Science Experience community](https://datascience.ibm.com/community). You can also navigate to the community from DSX by clicking the Community tab on the top panel.

<img src="https://cdn-images-1.medium.com/max/1600/1*Zmnd3s3ptuKeXzI-xURg6Q.png">

#### Step 2

Select the data set from the community and click the add (+) icon on the community card. Select your project and click Add.

<img src="https://cdn-images-1.medium.com/max/1600/1*12ZoPBRGJz65WUUzjTjhQw.png">

After you add the data set to your project you can find it in the Data assets section under the Assets tab.

<img src="https://cdn-images-1.medium.com/max/1600/1*uz0KBpdc0aSXMqQORUN62A.png">

## Tools
Data Science Experience offers an array of options for working with your data. To model this problem and understand the factors affecting chronic kidney disease, we will use IBM SPSS Modeler Flow in DSX. IBM SPSS Modeler Flow is a graphical interface to create different machine learning flows.

## Create SPSS Modeler Flow

#### Step 1
To create an SPSS Modeler Flow, go to the Assets tab as shown above and click the new flow icon under the SPSS Modeler Flow section.

#### Step 2
Give a name and description to the flow and select the IBM SPSS Modeler runtime.

<img src="https://cdn-images-1.medium.com/max/2000/1*zQkwoiOWO-0LfN9hXNTkSQ.png">

## Nodes
Before starting with the analysis, let’s have a look at different node options available in SPSS Modeler Flow.

On left side panel (Nodes Palette) you can see different types of nodes available for you to use while working on your data. There are six types of node categories.

1. **Record Operations:** As the name suggests, you can use them to perform operations such as selecting, appending, sorting on the record (row) level.

2. **Field Operations:** These nodes are helpful in the data preparation phase. You can filter data, rename features, and choose the type of your attributes.

3. **Graphs:** Nodes in this section will help you with basic data exploration and understanding distribution or relationship between features.

4. **Modeling:** These nodes provide different modeling algorithms for different types of problems.

5. **Outputs:** These nodes are helpful in understanding your data and model. You can display results in table format or get a report on evaluation parameters of your model.

6. **Export:** After processing and modeling, this node will help you export data from the flow editor to your DSX project.


Drag and drop the node into the canvas and right-click to take further actions such as open, preview, or run.

<img src="https://cdn-images-1.medium.com/max/1600/1*p1s7fjouFVgUhGzEoDMygg.png">

## Load Data
To start working on the problem, first we need to get data into the canvas. It is as easy as drag-and-drop. To preview the file, right-click on a node and select preview.

<img src="https://cdn-images-1.medium.com/max/1600/1*x8AdhFt3mzUC9JOQ7CrngQ.gif">


## Data Audit
In the data preview we saw that there are a few values missing from our data. Let’s dig deeper into summary statistics of our data using the Data Audit node.

1. Drag the Data Audit node and connect it with the data node.
2. Right click on the node and select open option to change settings or give a custom name. Hit save button at the bottom to save all changes.

<img src="https://cdn-images-1.medium.com/max/1600/1*XDnTEyBK7xw5YS90i9TheQ.png">

3.Right click on the node and select run option. After running the node you can see your audit report on right side panel.

<img src="https://cdn-images-1.medium.com/max/1600/1*9PqAN9xofsQF0-gd3DuxnA.png">

## Data Cleaning
In the audit report, we can see that few columns have missing value (?) as mode. This means in these columns missing value (?) occur most often. If we just delete all  rows with missing values, many rows will get deleted because of these columns.To retain more data we will drop these columns first and then drop rows with missing values.

#### Drop Columns
1. To drop columns drag and drop Filter node on the canvas and connect it with data node.
2. Right click and open the node. Select below columns under filter section
[bgr,sod,pot,hemo,pcv,wbcc & rbcc] make sure to check box - Filter selected fields and hit save button.

#### Drop Rows

1. Drag and drop Select node on the canvas, connect it with Filter node, right click and open the node.
2. Select discard mode and provide below condition to remove rows with missing values.

  (sg = '?' or al= '?' or su= '?' or rbc= '?' or pc= '?' or pcc= '?' or ba= '?' or bu= '?' or appet= '?' or pe= '?' or ane= '?')

Once our data is clean, we can set our class variable as the target variable using the Type node. It will help our model to distinguish between input and target features.

1. Drag and drop the Type node on the canvas, connect it with Select node, right click and open the node.
2. Click on configure types. Select column name class, change role to target hit ok and then save.

<img src="https://cdn-images-1.medium.com/max/1600/1*uxblb4ErZtidD83XbCPT4w.png">

## Distribution

Let’s take a quick look at the distribution of our target variable (class).
1. Drag the Distribution node from the graphs section of the node palette to the canvas and connect it with Type node.
2. Right click and open the node. Select column name class under field section. Under annotations give custom name  as target distribution and save the details.
3. Right click and run the Distribution node. It will generate plot which you will find on right hand side panel.

<img src="https://cdn-images-1.medium.com/max/1600/1*_4Rk0WoZLSnpx66dLhPtSQ.png">

In our data we have more non-chronic kidney disease cases than chronic kidney disease cases.

## Data Partition

One more step before building the classification model is to divide data into train and test sets. We will use the Partition node for this.

1. Select Partition node and connect it with Type node.
2. Open the node and provide 70 and 30 values to training and testing partition respectively. It will divide 70% of the data for training and 30% for testing.
3. Check *use unique field to assign partitions* box and provide field name class. This will make partition based on just one field (class). Hit save button after entering all details.

<img src="https://cdn-images-1.medium.com/max/1600/1*jR4Fo68THJWmeFBF7Tf_-w.png">

## Classification

Now let’s fit the classification model. We will be using a C5.0 algorithm to build a decision tree. A C5.0 model works by splitting the data based on the field that provides the maximum information gain.You can see node C5.0 under the Modeling section of the nodes palette.

1. Drag and drop C5.0 node on canvas, connect it with partition node and open it to change settings.
2. Under build options select custom and provide model name as Decision Tree. Make sure *Use partitioned data* box is checked and output type is decision tree.
3. Hit save button and run the node.

<img src="https://cdn-images-1.medium.com/max/1600/1*prYIQ9ZHIcopElAvrN0EUg.png">

While building this model we don’t have to specify input and output variables. We have already done that in the Type node.
Once you run your decision tree model you will be able to see your model in a golden color node.

## View Model

Right-click on the golden color node and view the model. You can see predictor importance, tree digram, and other model information here.

<img src="https://cdn-images-1.medium.com/max/1600/1*hm7jZPgTzp98Au1zvxYkSw.png">

## Model Evaluation

1. Select Analysis node from the Output section of the node palette and connect it with the model.

2. Right click to run the node and open results from right hand side panel. You can view data in a table format with predicted labels and confidence.


 <img src="https://cdn-images-1.medium.com/max/1600/1*ZfNF7ONehQEIwvnT_-qcIg.png">




 Similarly, use the Table node to view data in a table format with predicted labels and confidence.

<img src="https://cdn-images-1.medium.com/max/1600/1*4rWfyV1Y34_72QBjjfYfsw.png">


 This is the analysis report for our model.We have achieved 97% accuracy on our test data set with this model.

## Save Model

Now it’s time to save our model. Right click on a terminal node in the flow (e.g. analysis/table nodes) , click on save as a model option and provide model name to save this SPSS model to the project.

<img src="https://cdn-images-1.medium.com/max/1600/1*JTZx5JYq1OAORu5Gj4sFyA.png">


## Clustering

A great thing about SPSS Modeler Flow is that you can build different models within the same canvas.
Assume we don’t know if a person has chronic kidney disease or not. Let’s try to build an unsupervised model and see if we can identify pattern for chronic kidney disease.


1. Drag K-Means node to the canvas for this experiment and right click to open the node.
2.  Check *Use custom field roles* box and Select all features except class (target feature).
3. Set number of clusters to 2 under build options. We are expecting only two clusters here (chronic kidney disease & non-chronic kidney disease). Deselect *Use partitioned data* checkbox. Save the changes and run the node.

<img src="https://cdn-images-1.medium.com/max/1600/1*JSBvdWTWWV0lhXSHC1qG-Q.png">

## View Model

We can view model information by right-clicking the golden K-means node and selecting View model option.

<img src="https://cdn-images-1.medium.com/max/1600/1*g7cMM7Xlakoh9NorJUCI8g.png">


## Model Evaluation

Finally, let’s evaluate clustering results with respect to our original target labels.

1. Select Distribution node to the canvas and open it.
2. Select predicted cluster field ($KM-K-Means) under field section and select target variable (class) under color.
3. Give custom name, save the changes and run the node. Open the plot from right hand side panel.

<img src="https://cdn-images-1.medium.com/max/1600/1*gB3asQo4mAeebaWV6-Yzfg.png">


Here cluster-1 represents non-chronic kidney disease patients and cluster-2 belongs to patients who have this disease. Some people with chronic kidney disease are wrongly identified by the K- Means algorithm as non-chronic kidney disease patients.

## Export Results
Finally, to export your results use the Data Export node. Give a name to your file under the path section in the settings. Data will be exported to your project storage and you can see it under the Data Asset tab in the project.

<img src="https://cdn-images-1.medium.com/max/1600/1*-JNLJMtD6BI4kGpdqlJiLQ.png">


You can choose to run all flows on the canvas by using the run icon on the top panel. You can also take advantage of shortcuts such as copy, cut, and paste. To download your flow, click on the download icon from upper right side panel. This will download a SPSS Modeler .str file that can be opened in SPSS Modeler.

<img src="https://cdn-images-1.medium.com/max/1600/1*cHgXJivaDXhGqxwvivQOdw.png">

You can work on different problems by experimenting with different algorithms and modeling techniques in SPSS Modeler Flow.
