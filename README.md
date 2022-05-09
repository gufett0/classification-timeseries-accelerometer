# Smartphone accelerometer data for human activity classification

The completion of this project earned me a [verified certificate](https://courses.edx.org/certificates/c7b22364b2b94d5b83ff9566fba23070) from HarvardX. 
The goal was to provide the predicted physical activity based on tri-axial smartphone accelerometer data, which was collected from the Beiwe [research platform](https://github.com/onnela-lab/beiwe-backend). 

### Provided datasets

  - [train_labels.csv](https://github.com/gufett0/classification-timeseries-accelerometer/blob/main/train_labels.csv)
  - [train_time_series.csv](https://github.com/gufett0/classification-timeseries-accelerometer/blob/main/train_time_series.csv)
  - [test_time_series.csv](https://github.com/gufett0/classification-timeseries-accelerometer/blob/main/test_time_series.csv)
  - [test_labels.csv](https://github.com/gufett0/classification-timeseries-accelerometer/blob/main/test_labels.csv)

In the time series files the relevant columns are those labeled *x*, *y*, *z* for the othogonal axes of linear acceleration values and the *timestamp* for the tracking of time. The train accelerations dataset has 3744 rows Vs. 1250 of the test dataset.

In the train label file (375 rows) a number from 1 to 4 (i.e., 1=Standing, 2=Walking, 3=Stairs down, 4=Stairs up) is assigned to each time point. 
The test label file (175 rows) has empty cells to be filled with the predicted classes which were evaluated externally by the EdX platform.


### Main steps of my supervised ML approach


  1) **Exploring and cleaning data**. Two critical aspects emerged. Firstly, the different sampling rate between acceleration data (10 Hz, 1 data point every 0.1 second) and multi-label classification (1 Hz, 1 label every second) required a homogenization procedure such that each label has its own descriptor. Here acceleration data was filtered according to the timestamps of each given label, thus reducing the dataframe from 3744 to 375 rows. Secondly, a strong class imbalance was evident and had to be properly addressed.  
 
 2) **Modeling**. The 3 classification models covered in the course were also used here: *multinomial logistic regression*, *random forest classifier* and *nearest neighbors classifier*. Since accuracy alone is not optimal to evaluate imbalanced datasets (i.e., accuracy paradox), model selection was based on the average between Accuracy and F1-scores. Furthermore, the highest Cohen's kappa score, a value between -1 and 1, was assessed to further confirm the best model (kappa score represents accuracy normalized by the imbalance of the classes in the data).
 
 3) **SMOTE for Balancing Data**. Given the already small size of the train set, data was augmented (i.e., oversampled) for the minority classes. [SMOTE algorithm](https://machinelearningmastery.com/smote-oversampling-for-imbalanced-classification/) works by selecting examples that are close in the feature space, drawing a line between the examples in the feature space and drawing a new sample at a point along that line. Previously found best parameters (i.e., with cross validation randomized search) were again used to fit the model.

  ```
                  Accuracy	F1-scores	Kappa-scores
  Imbalanced data	0.722667	0.675894	0.458995
  SMOTE data	0.850939	0.848939	0.801252
  ```
Best model performance sensibly improved after balancing the data. The same model then was used to extract predicted labels on the test set.

### Improvement suggestions
   - Homogenization of data can be improved by replicating each label 10 times along time in order to have a more informed classifier training. 
   - Number of descriptors can be further increased by extracting statistical features of the 3-axes components (e.g., median, SD, kurtosis, 1st Fourier transform element) 

