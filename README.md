# Human-Activity-Recognition

This project is doing an analysis with R for "Human Activity Recognition Using Smartphones Data set".

## About Data Set
Whole data set comes from experiments which have been carried out with a group of 30 volunteers wearing a Samsung smartphone on the waist.Using its embedded accelerometer and gyroscope, experiments captured data of signals of 3-axial linear acceleration and 3-axial angular velocity.

For more explanation,please read "README.txt" and "features_info.txt" in the package of the data set.

## Project Tasks
1: Load the data in RStudio

2: Merge data sets
Merge the training and the test sets to create one data set.

3: Mean and standard deviation
Create two new columns, containing the mean and standard deviation for each measurement respectively.

4: Add new variables
Create variables called ActivityLabel and ActivityName that label all observations with the corresponding activity labels and names respectively

5: Create tidy data set
From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject. 

## Data Processing
1.For detail of data processing procedure,please read "CodeBook.md".

2.Some explanations for the data manipulation methods
* In merging section,I used a new column "train_test" as an identifier in all new merged dataframes.Then people still can identify which data record comes from train or from test.
* Subject_all,y_all and xdata_all will finally merge together to form into a new dataframe "subject_activity_features_all",which can be used to create a tidy dataframe for task 5.So I just put "train_test" column into y_train and y_test.
* For measurement data files such as "body_acc_x_train.txt",I add "train_test" column into related dataframes when I read thme into R.
* For task 3, I used related feature variables in xall_data to generate two columns of the mean and standard deviation for two kinds of dataframe:the body acceleration signal and the angular velocity vector. I did not find related features in xall_data for the total acceleration signal.
*To do task 4,I create a new column "activity_name" for y_all,and merge subject_all,y_all and xdata_all into subject_activity_features_all.
*To generate a tidy dataframe,I used aggregate function on subject_activity_features_all to create a tidy data set:tidy_data,and write it to a output .csv file"tidy_data.csv".



