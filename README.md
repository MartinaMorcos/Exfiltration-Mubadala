# KU-Mubadala Lab Exercise Using Weka
## Step 1: Download and Install Weka
* For Instructions on how to install Weka on your machine please follow this [link](https://machinelearningmastery.com/download-install-weka-machine-learning-workbench/)
## Step 2: Download the exfiltration data set (exfil_monograms_noisy.csv)
* The exfiltration dataset uses 20s histograms of the system calls to predict whether a process is malign (exfiltrating) or benign. The dataset consists of 99 input features/attributes which are the system call and 2 classes/labels with column name 'Label' in the csv file (0 for benign and 1 for malign). There are a total of 6,141 samples in the dataset (3,207 benign and 2,934 malign). All variable types are integers and correspond to the raw number of occurrence of each system call in a 20s time period.
## Step 3: View and convert to .arff format
* From the Weka GUI go to Tools-->ArffViewer
* In the ArffViewer change the file type to csv and open the exfil_monogram_noisy.csv file saved on your pc
* When the data set is opened go to File-->Save as and keep the file type as .arff
## Step 4: Open the .arff file and convert Label column to nominal
* From the Weka GUI start the Explorer and open your saved “exfil_monogram_noisy.arff”
* You will see all the attributes and the statistics for each upon selection
* Go to the last attribute “Label”, you will see that the data type is numeric but it should be changed to nominal (categorical) since this is the label for our data (0 for Benign and 1 for Malign)
* Click the “Choose” button for the Filter and select NumericToNominal, it is under unsupervised.attribute.
* After it is selected click on it to edit properties and make sure to change attributeIndices to **last** only <img src="https://github.com/MartinaMorcos/Exfiltration-Mubadala/blob/main/screenshots/nominal.png" height="400" width="430" >

* Click ok then apply filter. You can now see the distribution of data from each class. 
* You can now resave the data in this format
## Exercise 1: Compute regression to obtain the number of write (index 7) syscalls as a linear combination of openat (index 39) and read (index 5) syscalls numbers 
* You can remove all other attributes for this exercise
* You can view the instances for these three attributes from the Edit button
* You’ll notice after removing other attributes that there are a lot of duplicates so you can apply RemoveDuplicates filter under unsupervised.instance 
 <img src="https://github.com/MartinaMorcos/Exfiltration-Mubadala/blob/main/screenshots/rem_dupl.png" height="500" width="400" >
 
* You’ll find Linear Regression in the classifier tab under functions
* Make sure to output predictions as PlainText in order to see the difference between actual and predicted values and select **write** as the dependent variable 
 <img src="https://github.com/MartinaMorcos/Exfiltration-Mubadala/blob/main/screenshots/Ex1.png" height="380" width="520" >
 
* Get the equation of write as linear combination of read and openat
* Get the model’s performance metrics (correlation coefficient, RMSE, relative squared error, etc)
* Reload the data & repeat the previous exercise with the addition of more attributes in order to predict the write system call and compare the resulting error
* Notice if any system call attribute is assigned a coefficient of 0 after fitting the linear regressor

## Exercise 2: Use [3-sigma](https://en.wikipedia.org/wiki/68%E2%80%9395%E2%80%9399.7_rule) and the distribution of system calls to identify outliers/anomalous points
* Upon observation of the frequency distribution graphs of each syscall, you’ll notice that all of the syscalls are right skewed 
* Use sample statistics to transform right skew to bilateral using NumericTransform filter under unsupervised.attribute and select methodName as log10 and attributeIndices as 1-99 and then click apply
 <img src="https://github.com/MartinaMorcos/Exfiltration-Mubadala/blob/main/screenshots/Ex2.png" height="400" width="430" >

* Save transformed data as .csv file
* Use the transformed csv file and the [Kolmogorov-Smirnov Test of Normality](https://www.statskingdom.com/kolmogorov-smirnov-test-calculator.html) to check which syscalls are the closest to gaussian  <img src="https://github.com/MartinaMorcos/Exfiltration-Mubadala/blob/main/screenshots/Ex2-2.png" height="400" width="430" >

* Compute the 3-sigma intervals for the gaussian syscalls (use excel if needed)
	  
    𝜇−3𝜎≤𝑋≤𝜇+3𝜎
	
  Where 𝜇 is the mean, 𝜎 is the standard deviation and X is a single observation
* Propose a way on how to use these intervals for anomaly detection in a new dataset
## Exercise 3: Compute classification to distinguish benign from malign 
* Choose and train a baseline model for exfiltration dataset classification (ZeroR)
* Try different classifier algorithms such as J48, Random Forest, Decision Tree and Naïve Bayes
* Compare confusion matrix and accuracy 



