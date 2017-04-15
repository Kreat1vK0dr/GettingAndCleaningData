# UCI HAR Tidy Dataset

This dataset is derived from the UCI HAR Dataset.
Please see http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones.

## Methods
This dataset was constructed in R from the original UCI HAR Dataset using the following methods:

### Merging the datasets
- (1) Merged relational tables into single datasets for test and training data, respectively.
- (1.a) Achieved this by adding a common "id" column to the separate subject, feature-vector, and activity datasets for test and training data, respectively.
- (2) Used bind_rows (dplyr package) to bind test and training data into a single dataset, removing the previously created "id" column.
- (2.a) To keep only the mean and standard deviation measurements of each variable I used the grep function to create a logical vector of column names to keep.
### Creating the tidy dataset
- (3) Used melt function on the final dataset created above to transform column variables from the original dataset into a single "variable" column with their values in a "value" column.
- (4) The final step was to use a ddply function on the "melted" data, splitting by subject, activity and the newly created variable column passing "average=mean(value)" to the summarize function to achieve the average for each variable for each activity and for each subject.

## Variables

### id
Row reference.

### subject
An integer reference of the subject the measurements from the original dataset were taken from.

### activity
Description of the type of activity the subject performed while the measurements were taken.

### average
An average of the associated variable.

### variable
Name of the variable used from the original dataset.

```
> str(tidy_dataset)
'data.frame':	11880 obs. of  5 variables:
 $ id      : int  1 2 3 4 5 6 7 8 9 10 ...
 $ subject : int  1 1 1 1 1 1 1 1 1 1 ...
 $ activity: Factor w/ 6 levels "LAYING","SITTING",..: 1 1 1 1 1 1 1 1 1 1 ...
 $ variable: Factor w/ 66 levels "tBodyAcc-mean()-X",..: 1 2 3 4 5 6 7 8 9 10 ...
 $ average : num  0.2216 -0.0405 -0.1132 -0.9281 -0.8368 ...
 
> summary(tidy_dataset)
       id           subject                   activity                 variable        average        
 Min.   :    1   Min.   : 1.0   LAYING            :1980   tBodyAcc-mean()-X:  180   Min.   :-0.99767  
 1st Qu.: 2971   1st Qu.: 8.0   SITTING           :1980   tBodyAcc-mean()-Y:  180   1st Qu.:-0.96205  
 Median : 5940   Median :15.5   STANDING          :1980   tBodyAcc-mean()-Z:  180   Median :-0.46989  
 Mean   : 5940   Mean   :15.5   WALKING           :1980   tBodyAcc-std()-X :  180   Mean   :-0.48436  
 3rd Qu.: 8910   3rd Qu.:23.0   WALKING_DOWNSTAIRS:1980   tBodyAcc-std()-Y :  180   3rd Qu.:-0.07836  
 Max.   :11880   Max.   :30.0   WALKING_UPSTAIRS  :1980   tBodyAcc-std()-Z :  180   Max.   : 0.97451  
                                                          (Other)          :10800                     
> 
```
