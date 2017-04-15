# Coursera Course Project: Getting And Cleaning Data
This is a repository for the Coursera course 'Getting and Cleaning Data' course - part of the Coursera Data Science Specialisation.

## Submissions
### run_analysis.R
This is a script that reads and manipulates the data from the original UCI HAR Datasets to construct a new tidy data set.
It follows the following methods:

#### Methods
This dataset was constructed in R from the original UCI HAR Dataset using the following methods:

##### Merging the datasets
- (1) Merged relational tables into single datasets for test and training data, respectively.
- (1.a) Achieved this by adding a common "id" column to the separate subject, feature-vector, and activity datasets for test and training data, respectively.
- (2) Used bind_rows (dplyr package) to bind test and training data into a single dataset, removing the previously created "id" column.
- (2.a) To keep only the mean and standard deviation measurements of each variable I used the grep function to create a logical vector of column names to keep.
##### Creating the tidy dataset
- (3) Used melt function on the final dataset created above to transform column variables from the original dataset into a single "variable" column with their values in a "value" column.
- (4) The final step was to use a ddply function on the "melted" data, splitting by subject, activity and the newly created variable column passing "average=mean(value)" to the summarize function to achieve the average for each variable for each activity and for each subject.

### tidy_dataset.txt & tidy_dataset.csv
Exported copies of the dataset generated from the `run_analysis.R` script.

### CodeBook.md
Brief description of the methods used in obtaining the final tidy dataset as well as its variables.

### Before executing the script `run_analysis.R`  please `source` it in R:
`source("path/to/run_analysis.R")`
