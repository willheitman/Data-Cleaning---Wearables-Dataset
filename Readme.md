## Step 1 - Merge Training and Test Data Sets

#### Loads in needed libraries

```{r}

library(reshape2)

```

#### Reads in the three types of data sets (measurements, subjects, activity ids) for each of
#### the two types of data (test and train)

```{r}

testdata <- read.table("X_test.txt")
testnames <- read.table("Y_test.txt")
traindata <- read.table("X_train.txt")
trainnames <- read.table("Y_train.txt")
subjecttrain <- read.table("subject_train.txt")
subjecttest <- read.table("subject_test.txt")
features <- read.table("features.txt")

```

#### Combines the differenct pieces of data.  The first three lines vertically combine rows for
#### measurements, subjects, and activity ids.

```{r}

combinedsubject <- rbind(subjecttest,subjecttrain)
combinednames <- rbind(testnames,trainnames)
combineddata <- rbind(testdata,traindata)

```

#### The next three lines join columns so that measurements, subjects, and activity ids are all together
####  Then variable names are added in from the features file with subject and activity num appended to the front

```{r}

weardata <- cbind(combinedsubject,combinednames,combineddata)
varnames <- c("subject","activitynum",features$V2)
names(weardata) <- varnames

```

## Step 2 - Extract only mean and standard deviation for each measurement

#### grepl selects only those variables with that are means, standard deviations, or id columns

```{r}

weardata <- weardata[,grepl("mean()",names(weardata)) | grepl("std()",names(weardata)) | grepl("subject",names(weardata)) | grepl("activitynum",names(weardata))]
weardata <- weardata[,!grepl("meanFreq()",names(weardata))]

```

## Step 3 - Add descriptive activity names

#### Referencing the activity labels file, a small data frame with activity ids and matching activity labels
#### is created.  Then, this frame is merged with the main wearables frame

```{r}

activitylabels <- data.frame(activitynum = c(1:6),activity = c("Walking","walking upstairs","walking downstairs","sitting","standing","laying"))
weardata <- merge(activitylabels,weardata,by.x = "activitynum",by.y = "activitynum", all = TRUE)

```

## Step 4 - Add descriptive variable labels

#### In order to clean up variable labels, "t" and "f" are replaced with "time" and "frequency".
#### Mean() and std() have superfluous parentheses removed.  
#### Variable labels are changed to all lowercase in accordance with best practices.  
#### X,Y,Z changed to xaxis,yaxis, and zaxis for added clarity

```{r}

names(weardata) <- sub("tBody","timebody",names(weardata))
names(weardata) <- sub("fBody","frequencybody",names(weardata))
names(weardata) <- sub("tGravity","timegravity",names(weardata))
names(weardata) <- sub("mean\\(\\)","mean",names(weardata))
names(weardata) <- sub("std\\(\\)","std",names(weardata))
names(weardata) <- tolower(names(weardata))
names(weardata) <- sub("bodybody","body",names(weardata))
names(weardata) <- sub("-x","-xaxis",names(weardata))
names(weardata) <- sub("-y","-yaxis",names(weardata))
names(weardata) <- sub("-z","-zaxis",names(weardata))

```

## Step 5 - Create second, independent tidy data set with avg for each activity and subject

#### First, melts the weardata frame down using activty and subject as ids
#### Second, casts the melted frame using the ids with mean as the summary operation.
#### This results in a data frame with the mean for every combination of activity, subject, and measurement.

```{r}

wearmelt <- melt(weardata[,2:69],id=c("activity","subject"),measure.vars = names(weardata[,4:69]))
finalwearabledata <- dcast(wearmelt,activity+subject~variable,mean)

```

#### Writes csv with final data

```{r}

write.table(finalwearabledata,"finalwearable.txt",row.name=FALSE)

```

#### We are done!