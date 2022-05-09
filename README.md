# Smartphone accelerometer data for human activity classification

The completion of this project earned me a [verified certificate](https://courses.edx.org/certificates/c7b22364b2b94d5b83ff9566fba23070) from HarvardX. 
The goal was to provide the predicted physical activity based on tri-axial smartphone accelerometer data, which was collected from the Beiwe [research platform](https://github.com/onnela-lab/beiwe-backend). 

### Provided datasets

  - [train_labels.csv](https://github.com/gufett0/classification-timeseries-accelerometer/blob/main/train_labels.csv)
  - [train_time_series.csv](https://github.com/gufett0/classification-timeseries-accelerometer/blob/main/train_time_series.csv)
  - [test_time_series.csv](https://github.com/gufett0/classification-timeseries-accelerometer/blob/main/test_time_series.csv)
  - [test_labels.csv](https://github.com/gufett0/classification-timeseries-accelerometer/blob/main/test_labels.csv)

In the time series files the relevant columns are those labeled *x*, *y*, *z* for the othogonal axes of linear acceleration values and the *timestamp* for the tracking of time. The train dataset has 3744 rows Vs. 1250 of the test dataset.

In the train label file (375 rows) a number from 1 to 4 (i.e., 1=Standing, 2=Walking, 3=Stairs down, 4=Stairs up) is assigned for each time point. 
The test label file (175 rows) has empty cells to be filled with the predicted classes which were evaluated externally by the EdX platform.


### Main steps of my supervised ML approach


  1) **Exploring and cleaning data**. Two critical aspects emerge. Firstly, it's the different sampling rate between acceleration data (10 Hz, 1 data point every 0.1 second) and multi-label classification (1 Hz, 1 label every second) requiring a homogenization procedure such that each label has its own descriptor. Here acceleration data was filtered according to the timestamps of each given label, thus reducing the dataframe from 3744 to 375 rows. Secondly, a strong class imbalance was evident and had to be addressed appropriately.  
  2) **Modeling**. Three classification models that were covered in the course: *multinomial logistic regression*, *random forest classifier* and *nearest neighbors classifier*.

