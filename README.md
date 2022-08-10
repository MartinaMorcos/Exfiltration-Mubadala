# KU-Mubadala Lab Example Using Weka
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
* After it is selected click on it to edit properties and make sure to change attributeIndices to **last** only ![alt text](https://github.com/MartinaMorcos/Exfiltration-Mubadala/screenshots/nominal.png)

* Click ok then apply filter. You can now see the distribution of data from each class. 
* You can now resave the data in this format

