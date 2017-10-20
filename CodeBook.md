Introduction
============

It's a book to describe how run\_analysis.R is running to read data,combine data,create new columms,and group data into a tidy data set.

There are those code sections below: 1.Origin data source link 2.Including Libraries 3.Function and constants 4.Reading data 5.Data manipulation 6.Writing output csv file for tidy data set

Part I:Data Source Link
=======================

<https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip>

Part II:Libraries
=================

Use three libraries:tidyr,dplyr,stringr

Part III: Funtions and constonts
================================

-   Functions Just use one function to create a activity name vector for any dataframe which has a column contained activity label vector.

-   Constants There are two constonts as identifier for data set comes from train or test:train\_flag="1",test\_flag="0".

Part IV:Read data
=================

This section will read .txt files from "./samsung/" (if change this directory,you need to change some codes below )

-   Read activity\_labels.txt into Data frame:activity\_labels
-   Read features.txt into Data frame:features \#\#Read Train Data
-   Read X\_train.txt into Data frame:xtrain\_data,and use vector data at second column of feature as columns' name at same time.
-   Read subject\_train.txt.txt into Data frame:subject\_train,and give the only column a name:"subject"
-   Read y\_train.txt into Data frame:y\_train,and give the only column a name:"activity\_label"
-   Read body\_acc\_x\_train.txt into Data frame:body\_acc\_x\_train, and add new column:train\_test as identifier
-   Read body\_acc\_y\_train.txt into Data frame:body\_acc\_y\_train, and add new column:train\_test as identifier
-   Read body\_acc\_z\_train.txt into Data frame:body\_acc\_z\_train, and add new column:train\_test as identifier
-   Read body\_gyro\_x\_train.txt into Data frame:body\_gyro\_x\_train, and add new column:train\_test as identifier
-   Read body\_gyro\_y\_train.txt into Data frame:body\_gyro\_y\_train, and add new column:train\_test as identifier
-   Read body\_gyro\_z\_train.txt into Data frame:body\_gyro\_z\_train, and add new column:train\_test as identifier
-   Read total\_acc\_x\_train.txt into Data frame:total\_acc\_x\_train, and add new column:train\_test as identifier
-   Read total\_acc\_y\_train.txt into Data frame:total\_acc\_y\_train, and add new column:train\_test as identifier
-   Read total\_acc\_z\_train.txt into Data frame:total\_acc\_z\_train, and add new column:train\_test as identifier \#\#Read Test Data
-   Read X\_test.txt into Data frame:xtest\_data,and use the data vector at second column of feature as columns' name
-   Read subject\_test.txt into Data frame:subject\_test,and give the only column a name:"subject"
-   Read y\_test.txt.txt into Data frame:y\_test,and give the only column a name:"activity\_label"
-   Read body\_acc\_x\_test.txt into Data frame:body\_acc\_x\_test, and add new column:train\_test as identifier
-   Read body\_acc\_y\_test.txt into Data frame:body\_acc\_y\_test, and add new column:train\_test as identifier
-   Read body\_acc\_z\_test.txt into Data frame:body\_acc\_z\_test, and add new column:train\_test as identifier
-   Read body\_gyro\_x\_test.txt into Data frame:body\_gyro\_x\_test, and add new column:train\_test as identifier
-   Read body\_gyro\_y\_test.txt into Data frame:body\_gyro\_y\_test, and add new column:train\_test as identifier
-   Read body\_gyro\_z\_test.txt into Data frame:body\_gyro\_z\_test, and add new column:train\_test as identifier
-   Read total\_acc\_x\_test.txt into Data frame:total\_acc\_x\_test, and add new column:train\_test as identifier
-   Read total\_acc\_y\_test.txt into Data frame:total\_acc\_y\_test, and add new column:train\_test as identifier
-   Read total\_acc\_z\_test.txt into Data frame:total\_acc\_z\_test, and add new column:train\_test as identifier

Part V:Data Manipulation
========================

Combine data from train and test
--------------------------------

-   Create a new column "train\_test" for y\_train as identifire for train data or test data
-   Create a new column "train\_test" for y\_test as identifire for train data or test data
-   Use rbind to combine y\_train and y\_test into a new dataframe:y\_all

-   Use rbind to combine subject\_train and subject\_test into a new dataframe:subject\_all

-   Use rbind to combine xtrain\_data and xtest\_data into a new dataframe:xall\_data xall\_data &lt;- rbind(xtrain\_data,xtest\_data)

-   combine all measurements data from train and test,such as:

    ``` r
    body_acc_x_all <- rbind(body_acc_x_train,body_acc_x_test)
    ```

    ...

    ``` r
    body_gyro_x_all <- rbind(body_gyro_x_train,body_gyro_x_test)
    ```

    ...

    ``` r
    total_acc_x_all <- rbind(total_acc_x_train,total_acc_x_test)
    ```

    ...

Add mean,std columns to body\_acc and body\_gyro measurement files
------------------------------------------------------------------

Such as:

``` r
body_acc_x_all[[make.names(c("tBodyAcc-mean()-X"), unique = TRUE)]]<-xall_data$tBodyAcc.mean...X
body_acc_x_all[[make.names(c("tBodyAcc-std()-X"), unique = TRUE)]]<-xall_data$tBodyAcc.std...X
```

...

``` r
body_gyro_x_all[[make.names(c("tBodyGyro-mean()-X"), unique = TRUE)]]<-xall_data$tBodyGyro.mean...X
body_gyro_x_all[[make.names(c("tBodyGyro-std()-X"), unique = TRUE)]]<-xall_data$tBodyGyro.std...X
```

Create a new observation dataframe with a new column "activity\_name".
----------------------------------------------------------------------

-   Create a new column "activity\_name" to y\_all,use "activity\_label" column to match names from activity\_labels
-   Use bind\_cols to merge y\_all and subject\_all into subject\_acitivity\_all
-   Use bind\_cols to merge subject\_activity\_all and xall\_data into subject\_activity\_features\_all,which has more completed information.

Create a tidy data set with the average of each variable for each activity and each subject
-------------------------------------------------------------------------------------------

-   Use aggregate function to compute mean values for all feature columns in subject\_activity\_features\_all,group by two columns:"subject and "activity\_label",and then create a tidy data set:tidy\_data.
-   Add a "activity\_name" column after column "activity\_label" in tidy\_data.

Part VI:Write output .csv file
==============================

Write tidy\_data to tidy\_data.csv
