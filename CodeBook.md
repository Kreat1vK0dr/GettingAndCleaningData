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

### subject
An integer reference to the subject the measurements from the original dataset were taken from.

### activity
Description of the type of activity the subject performed while the measurements were taken.

### average
An average of the associated variable.

### variable
Name of the variable used from the original dataset.
