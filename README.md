
## First Project

### Title: Playlist Classification Machine

Description: Predicting the genre (class) of a playlist using the audio features.

Data: Extracted from the "Spotifyr" package in R. 

<ins>Dependent Variable:</ins> _(Eight Genres)_  
- Rap/HipHop
- Synth
- Jazz
- Anime Openings
- Pop
- Classical Music
- Russian Turbo Polka
- Frenchcore

<ins>Predictors:</ins> _(Independent Variables/Features)_
- Loudness
- Speechiness
- Acousticness
- Instrumentalness
- Tempo
- Liveness
- Mode
- Danceability
- Energy
- Key
- Valence
- Track Popularity

<ins>Methods and Models employed:</ins> 
Linear Discriminant Analysis (LDA) and Leave One Out Cross-Validation (LOOCV)

<ins>Model Evaluation:</ins> 
Sensitivity, Specificity, Accuracy, Precision, Negative Predictive Value, and Accuracy 

<ins>Data Summary:</ins> 
- 500 songs
- 12 predictors
- 8 genres

<ins>Results:</ins> 
Overall Model Accuracy = 76 %


#### Kaggle Competitions 

## Second Project

### Title: Physical Activity Recognition

Description: Building a classifier that recognizes different types of physical activity from signals measured by the accelerometer and gyroscope in a smartphone, which both measure aspects of movement and orientation. 

Data: Collected in a lab using a basic smartphone in experiments with human participants carrying out various daily activities in set order.
The experiments were carried out with a group of 30 volunteers within an age bracket of 19-48 years. They performed a protocol of activities composed of six basic activities: three static postures (standing, sitting, lying) and three dynamic activities (walking, walking downstairs and walking upstairs). The experiment also included postural transitions that occurred between the static postures. These are: stand-to-sit, sit-to-stand, sit-to-lie, lie-to-sit, stand-to-lie, and lie-to-stand. All the participants were wearing a smartphone (Samsung Galaxy S II) on the waist during the experiment execution. We captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz using the embedded accelerometer and gyroscope of the device. The experiments were video-recorded to label the data manually. The obtained dataset was randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data.

Thanks to: 
Jorge L. Reyes-Ortiz1,2, Davide Anguita1, Luca Oneto1 and Xavier Parra2

Smartlab, DIBRIS - Universitá degli Studi di Genova, Genoa (16145), Italy.
CETpD - Universitat Politécnica de Catalunya. Vilanova i la Geltr˙ (08800), Spain har '@' smartlab.ws www.smartlab.ws

<ins>Dependent Variable:</ins> _(Twelve Physical Activities)_  
- walking
- walking upstairs
- walking downstairs
- sitting
- standing
- laying
- stand to sit
- sit to stand
- sit to lie
- lie to sit
- stand to lie
- lie to stand

<ins>Predictors:</ins> _(Independent Variables/Features)_

Signals were split into epoches containing 128 samples. I analyzed the histograms of the signals to design specific features that distinguish betweeen the different signals of physical activity. Overall the features could distinguish well, although it was very hard to do that for the following shifts:
- The time shift when someone starts to walk
- The time shift or delation when someone goes from walking slow to fast
- The amplitute shift where someone goes from taking 'normal steps' to smaller steps. 

I tried to design features that could help identifying the overall signals from the histograms, as well as the shifts that are more difficult to distinguish. Therefore, I designed the following features:

Features that capture the specific region
- Mean
- Mode
- Median
- Minimum
- Maximum
- Maximum Frequency Index

Features that capture specific spreading
- Power: the power is the probability that the test will find a statistically significant difference betIen the amplitude of the signals. Where it reflects the variance of the amplitude of the signals as Ill as the squared mean summed.
- MinMax: The difference betIen largest and smallest value in the histogram which is useful for differentiating betIen the spreads of the histograms (Bayat, Pomplun & Tran, 2014). 
- Mean Absolute Deviation (MAD): The absolute average distance betIen the mean and every data point. 

Features that capture specific statistics
- Standard Deviation
- Standard Error
- Interquartile Ranges
- 25% Quartile Ranges
- 75% Quartile Ranges

Features that capture specific shapes
- Skewness: Skewness is measured by identifying assymmetry of a particular histogram. The histogram is balanced when there is zero-value. It is on the left tail when it is negative, and it is on the right tail when it is positive. 
- Kurtosis: This measure describes the specific shape of a particular histogram where this shape is identified by measuring the peakedness of the histogram. If it's a normal distribution the peakedness is 3, which means that the most values are in and around the middel of the distribution. If it is not normal distributed the peakedness of the histogram, ans thus the most values are in the sides. 
- Entropy: According to the article "feature extraction from signals" entropy is a important measure of detecting signals and thus I also carried out this measurement.

Features that capture specific time domains
- Lagged cross-correlations: Cross-correlations are very useful in predicting the change of one  signal into another,specifically for comparing two times series or one in case of autocorrelations to see how Ill they match with one another. High correlations will indicate similarities betIen signals, whereas low will indicate no relation betIen the phenomena in the signals. This method takes into account time delay and thus allows to match certain signals that might have been overlooked otherwise. These differences thus alloId for further possible feature extraction and disentangling possible differences among signals. In my case, I decided to use different lags in order to cover as many possible scenarios (I used lags of 1, 3, 5, 10). Although it is more likely that as the number of lags increases, the possibility of a match decreases, I still deciced to test out a lag of 10 in order to possibly detect any potential matches. Source: https://www.usna.edu/Users/oceano/pguth/md_help/html/time0alq.htm
- Correlation: Computes the overall correlation betIen time series with no particular lags specified.
- Amplituderange: Computes the amplitude range which is the difference betIen the maximum and minimum sample values in a sample window. 
- MSE: The absolute sum of the signals. Computes the absolute area by taking the sum of the absolute sample values in a vector of signals. I found this was a useful measurement of time (Konsolakis, 2018). 
- Mean Frequency Average: Again Bakram and colleagues (2014) found this to be a good feature of physical activity recognition.
- Cosine Angles: Computes the cosine similarity betIen two vectors without taking into consideration their length. 

Features that capture specific frequencies
- Spectral features: The function spectrum() gives an estimation of the spectrum of a function. In order to be able to derive information about the nature of the function and more about the physical movements within my frequency domains, I estimated statistical features on the spectrum features. In particular I included features such as: spectral peak of a vector, spectral mean of a vector, spectral standard deviation of a vector, spectral entropy of a vector, spectral skewness and kurtosis of a vector, spectral mode and median of a vector. 
- Zero-crossings: The frequency of certain physical activities crossing a zero-point. Since I assume differenct physical activities and their signals differ in their frequency of zero-point crossings (Gangadhar, Giridhar Akula, & Reddy, 2018). 

** **
- Bayat, A., Pomplun, M., & Tran, D. A. (2014). A Study on Human Activity Recognition Using Accelerometer Data from Smartphones. Procedia Computer Science, 34, 450–457. https://doi.org/10.1016/j.procs.2014.07.009
- Gangadhar, Y., Giridhar Akula, V., & Reddy, P. C. (2018). An evolutionary programming approach for securing medical images using watermarking scheme in invariant discrete wavelet transformation. Biomedical Signal Processing and Control, 43, 31–40. https://doi.org/10.1016/j.bspc.2018.02.007
- Konsolakis, K. (2018). Physical Activity Recognition Using Wearable Accelerometers in Controlled and Free-Living Environments (Nr. 6). TU Delft. http://resolver.tudelft.nl/uuid:af2e1786-ccc4-4592-afc8-b19819544f26

<ins>Methods and Models employed:</ins> 
I fitted an LDA, KNN, KNNS (knn scaled), and a multinomial and QDA with less features because they only worked that way. When I added more features, the QDA and multinomial stopped working. Important to note is that I chose a K of 10, because Hastie and Tibshirani explained that the best K to choose is between 5 and 10, I went for a K of 10 in order to have large variance in my data. The split of 80/20 was chosen because it was mentioned in the book Introduction to Statistical Learning (James et. al, 2013) that the possibility of bias will become high when there is less data to train on. 

Thus, models and techniques employed were: 
- Linear Discriminant Model (LDA)
- K-Nearest Neighbour (KNN)
- K-Nearest Neighbour scaled (KNNs)
with K-fold (using 10 folds and a 80/20 split (training set vs test set) 

Additionally, variations of the aforementioned models were employed. Three types mainly: including all features, including only features that did not have high correlations with other features (collinearity), and those where some interaction terms were used (only for LDA). This resulted in 7 different models (LDA_all, LDA_clean, LDA_int, KNN_all, KNN_clean, KNNs_all, and KNNs_clean).

<ins>Model Evaluation and Model Comparison:</ins> 
LDA was chosen as the final model due to the highest *accuracy* compared to the other models.

<ins>Results:</ins> 
Results on the Kaggle competition showcased a total of 80.915% accuracy.

