# Codebook for Wearables Data

## Data Source

Jorge L. Reyes-Ortiz(1,2), Davide Anguita(1), Alessandro Ghio(1), Luca Oneto(1) and Xavier Parra(2)
1 - Smartlab - Non-Linear Complex Systems Laboratory
DITEN - Università degli Studi di Genova, Genoa (I-16145), Italy.
2 - CETpD - Technical Research Centre for Dependency Care and Autonomous Living
Universitat Politècnica de Catalunya (BarcelonaTech). Vilanova i la Geltrú (08800), Spain
activityrecognition '@' smartlab.ws

## Raw Data

From the original codebook:

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

tBodyAcc-XYZ
tGravityAcc-XYZ
tBodyAccJerk-XYZ
tBodyGyro-XYZ
tBodyGyroJerk-XYZ
tBodyAccMag
tGravityAccMag
tBodyAccJerkMag
tBodyGyroMag
tBodyGyroJerkMag
fBodyAcc-XYZ
fBodyAccJerk-XYZ
fBodyGyro-XYZ
fBodyAccMag
fBodyAccJerkMag
fBodyGyroMag
fBodyGyroJerkMag

The set of variables that were estimated from these signals are: 

mean(): Mean value
std(): Standard deviation
mad(): Median absolute deviation 
max(): Largest value in array
min(): Smallest value in array
sma(): Signal magnitude area
energy(): Energy measure. Sum of the squares divided by the number of values. 
iqr(): Interquartile range 
entropy(): Signal entropy
arCoeff(): Autorregresion coefficients with Burg order equal to 4
correlation(): correlation coefficient between two signals
maxInds(): index of the frequency component with largest magnitude
meanFreq(): Weighted average of the frequency components to obtain a mean frequency
skewness(): skewness of the frequency domain signal 
kurtosis(): kurtosis of the frequency domain signal 
bandsEnergy(): Energy of a frequency interval within the 64 bins of the FFT of each window.
angle(): Angle between to vectors.

Additional vectors obtained by averaging the signals in a signal window sample. These are used on the angle() variable:

gravityMean
tBodyAccMean
tBodyAccJerkMean
tBodyGyroMean
tBodyGyroJerkMean

## Processed Data

Only means and standard deviations + activity and subject were kept from the original dataset.  This left a total of 68 variables as follows:


"activity"                        "subject"                        
"timebodyacc-mean-xaxis"          "timebodyacc-mean-yaxis"         
"timebodyacc-mean-zaxis"          "timebodyacc-std-xaxis"          
"timebodyacc-std-yaxis"           "timebodyacc-std-zaxis"          
"timegravityacc-mean-xaxis"       "timegravityacc-mean-yaxis"      
"timegravityacc-mean-zaxis"       "timegravityacc-std-xaxis"       
"timegravityacc-std-yaxis"        "timegravityacc-std-zaxis"       
"timebodyaccjerk-mean-xaxis"      "timebodyaccjerk-mean-yaxis"     
"timebodyaccjerk-mean-zaxis"      "timebodyaccjerk-std-xaxis"      
"timebodyaccjerk-std-yaxis"       "timebodyaccjerk-std-zaxis"      
"timebodygyro-mean-xaxis"         "timebodygyro-mean-yaxis"        
"timebodygyro-mean-zaxis"         "timebodygyro-std-xaxis"         
"timebodygyro-std-yaxis"          "timebodygyro-std-zaxis"         
"timebodygyrojerk-mean-xaxis"     "timebodygyrojerk-mean-yaxis"    
"timebodygyrojerk-mean-zaxis"     "timebodygyrojerk-std-xaxis"     
"timebodygyrojerk-std-yaxis"      "timebodygyrojerk-std-zaxis"     
"timebodyaccmag-mean"             "timebodyaccmag-std"             
"timegravityaccmag-mean"          "timegravityaccmag-std"          
"timebodyaccjerkmag-mean"         "timebodyaccjerkmag-std"         
"timebodygyromag-mean"            "timebodygyromag-std"            
"timebodygyrojerkmag-mean"        "timebodygyrojerkmag-std"        
"frequencybodyacc-mean-xaxis"     "frequencybodyacc-mean-yaxis"    
"frequencybodyacc-mean-zaxis"     "frequencybodyacc-std-xaxis"     
"frequencybodyacc-std-yaxis"      "frequencybodyacc-std-zaxis"     
"frequencybodyaccjerk-mean-xaxis" "frequencybodyaccjerk-mean-yaxis"
"frequencybodyaccjerk-mean-zaxis" "frequencybodyaccjerk-std-xaxis" 
"frequencybodyaccjerk-std-yaxis"  "frequencybodyaccjerk-std-zaxis" 
"frequencybodygyro-mean-xaxis"    "frequencybodygyro-mean-yaxis"   
"frequencybodygyro-mean-zaxis"    "frequencybodygyro-std-xaxis"    
"frequencybodygyro-std-yaxis"     "frequencybodygyro-std-zaxis"    
"frequencybodyaccmag-mean"        "frequencybodyaccmag-std"        
"frequencybodyaccjerkmag-mean"    "frequencybodyaccjerkmag-std"    
"frequencybodygyromag-mean"       "frequencybodygyromag-std"       
"frequencybodygyrojerkmag-mean"   "frequencybodygyrojerkmag-std"   

Activity is a factor describing the measured physical activity in one of six values

Subject is the integer id of each of the individuals participating in the study

Other variables are all numerics representing measurements as described in the raw section above.  Their names have been cleaned up vs their formats in the raw data.  "t" and "f" have been changed to "time and "frequency".  "x","y", and "Z" have
been changed to xaxis, yaxis, and zaxis for easier readability.  Names have been changed to all lower case for ease of use.  Parentheses have been removed
from variables names for easier reading.

Finally, a new dataset has been created from the original raw dataset.  Variables names remain the same, but values have been averaged for each combination of measurement, subject, and activity.  This has been accomplished using melt and dcast (see run_analysis.R)
