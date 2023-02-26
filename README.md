
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

References
** **
Bayat, A., Pomplun, M., & Tran, D. A. (2014). A Study on Human Activity Recognition Using Accelerometer Data from Smartphones. Procedia Computer Science, 34, 450–457. https://doi.org/10.1016/j.procs.2014.07.009
Gangadhar, Y., Giridhar Akula, V., & Reddy, P. C. (2018). An evolutionary programming approach for securing medical images using watermarking scheme in invariant discrete wavelet transformation. Biomedical Signal Processing and Control, 43, 31–40. https://doi.org/10.1016/j.bspc.2018.02.007
Konsolakis, K. (2018). Physical Activity Recognition Using Wearable Accelerometers in Controlled and Free-Living Environments (Nr. 6). TU Delft. http://resolver.tudelft.nl/uuid:af2e1786-ccc4-4592-afc8-b19819544f26


## Third Project

### Title: Personality Profiling of Youtube Vloggers

Description: Building a model that will predict scores on the Big Five Personality Traits of Youtube Vloggers using different aspects of their videos. 

Data: The YouTube personality dataset consists of a collection of behavorial features, speech transcriptions, and personality impression scores for a set of 404 YouTube vloggers that explicitly show themselves in front of the a webcam talking about a variety of topics including personal issues, politics, movies, books, etc. There is no content-related restriction and the language used in the videos is natural and diverse. For 80 of the 404 vloggers the personality impression scores are missing. The model is used to predict scores for these 80 vloggers.

<ins>Dependent Variable:</ins> _(Big Five Personality Traits)_  
- Extraversion
- Neuroticism
- Conscientiousness 
- Agreeableness
- Openess to Experience

<ins>Predictors:</ins> _(Independent Variables/Features)_

The predictors stemmed from three different aspects:
1) Speech transcripts
2) AudioVisual remarks (behavioural aspects) 
3) Personality scores of other vloggers

Based on the aforementioned, I constructed the following features:

Features derived from the speech transcript texts: 

- Number of times the word "um" is used
  - The first feature is the number of times the words "um", "uhm", and "uh" are used. These are so called filler words to avoid silences. Even though a direct    
    relationship between the use of filler words could not be shown in earlier research (Laserna et al., 2014), they could still indicate difficulty finding words     to say which might be related to for example introversion.
- NRC lexicon
  -The second feature is the NRC. The NRC is a large database that enables us to associate words with 8 common emotions, which are either negative or positive. How    much each emotion occurs in a text might tell us something about the personality of the speaker. In earlier research sentiment analysis using NRC was shown to      be an effective personality predictor (Christian et al. 2021).
- Bing lexicon
  - The third feature is Bing. Bing doesn't allow us to assign emotions to a word but it does let us classify words as positive or negative. The number of words in     a text that are positive or negative might also tell us something about de personality of the speaker. Also since the distribution of postive and negative     
    words is different in Bing than in NRC it seems sensible to use both.
- Count of Syllables 
  - The sixth feature is the number of syllables that each vlogger uses. Earlier research has shown that this is an effective predictor for mainly agreeableness
   (Metha et al., 2020). Even though this study was on written text, this finding might also hold for speech.
- Number of questions
  - The seventh feature is the number of questions in a vlog. Asking questions might for example be related to insecurity and thus introversion or to curiousness   
    and thus opnenness to experience.
- Swear words 
  - The eight feature is the number of swear words that is used. The study of Metha et al. 2020 also showed this was an effective predictor for agreeabless
    Besides that it also intuitively makes sense that the number of swear words would predict agreeableness (the more swear words the lower agreeableness)
    and possibly other big five traits. 
- Number of pauses
  - The ninth feature is the number of pauses for each vlogger. Since there are a lot of ways pauses or silence can be used in speech Kostiuk (2012) so it might       predict personality in different ways. However if there are a lot of pauses this likely indicates difficulty finding words which might be associated with           introversion. 
- Self-Reference/"I" Words 
  - Our tenth feature is the use of self-reference words. Self-reference words are associated with multiple personality traits so their use might be a good
    predictor for the Big Five. Earlier research showed for example an association between the use of the word "I" and neuroticism (Scully & Terry, 2011). 
- Some additional features based on similar reasoning: 
  - "We" Words Relative Frequency 
  - Average Number of characters in a sentence
  - AFINN 
  - Negation frequency
  - Mean Word Count Per Sentence

<ins>Methods and Models employed:</ins> 
- Here I employed a linear model along with stepwise regression methods (using the forward and the hybrid approach). Additionally, an alternative model with non-linear transformations was fitted in order to potentially increase the explained variance, and was thus compared to the primary model that does not violate the assumption of additivity. 

<ins>Model Evaluation and Model Comparison:</ins> 
- The simple model with no non-linear transformations had the highest explained variance, thus this model was used for prediction purposes.

<ins>Results:</ins>
My model explained 76% of the variance in Big Five Personality Traits scores using a test set.

<ins>References:</ins>

Christian, H., Suhartono, D., Chowanda, A., & Zamli, K. Z. (2021). Text based personality prediction from multiple social media data sources using pre-trained language model and model averaging. Journal of Big Data, 8(1). https://doi.org/10.1186/s40537-021-00459-1

Lee, C. H., Kim, K., Seo, Y. S., & Chung, C. K. (2007). The Relations Between Personality and Language Use. The Journal of General Psychology, 134(4), 405–413. https://doi.org/10.3200/genp.134.4.405-414

Laserna, C. M., Seih, Y. T., & Pennebaker, J. W. (2014). Um . . . Who Like Says You Know. Journal of Language and Social Psychology, 33(3), 328–338. https://doi.org/10.1177/0261927x14526993

Mehta, Y., Fatehi, S., Kazameini, A., Stachl, C., Cambria, E., & Eetemadi, S. (2020). Bottom-Up and Top-Down: Predicting Personality with Psycholinguistic and Language Model Features. 2020 IEEE International Conference on Data Mining (ICDM). Published. https://doi.org/10.1109/icdm50108.2020.00146

Scully, I. D., & Terry, C. P. (2011). Self-Referential Memory for the Big-Five Personality Traits. Psi Chi Journal of Psychological Research, 16(3), 123–128. https://doi.org/10.24839/1089-4136.jn16.3.123

## Fourth Project

### Title: Customer Satisfaction from Amazon Reviews 

Description: Here I tried to build a classifier that automatically recognizes customer satisfaction from textual reviews of baby products that were sold on Amazon.com.

Data: Reviews and 5 star ratings were collected by Amazon on their site by inviting customers to enter a review of a product that had bought. The extracted data from Amazon contains: the item described, the review text as a (long) string, and a numeric rating. Customers are assumed the be “satisfied” if the numeric rating is greater than the midpoint of the scale.

<ins>Dependent Variable:</ins> _(Satisfaction)_

Level of satisfaction of customers, ranging from 1 to 5.

<ins>Predictors:</ins>  (Independent Variables/Features)

Features were extracted from tokenized (words) text transcripts.

The constructed features:

- Term Frequency - Inverse Document Frequency Features
- The TF-IDF based on single words, without filtering for the stopwords
- The TF-IDF based on bigrams, which we also did not filter on stopwords. We found this to be a very useful feature for sentiment analysis (Tan, Wang & Lee, 2002).
- The TF-IDF based on trigrams also without filtering for the stopwords. Again, trigrams were also found to be useful feature for sentiment analysis (Wu, Li, & Xu, 2006).

The following process was employed:

- document occurence:
  - 0-1 encoding of the presence or absence of a token t in a document n (here: review)
- token counts:
  - simple counts of each token t within documents (resulting in a document by term matrix, or DTM)
- term frequency (TF):
  - then calculate the relative frequency of a token t within a document n
- inverse document frequency (IDF):
  - inverse the relative frequency with which a term occurs among the N documents, expressed on a log scale (a measure of ‘surprise’) calculated by
    dividng the number of documents that contain the token _t_over the number of total number of documents (N).
- the TFIDF:
  - the product of TF and IDF
   
The motivation for TF is simply that the more often a token t occurs in a document, the more likely it is that the topic of the document is closely related to that token. A problem of TF is that it does not take into account that certain words simply occur more frequently because of their role in language (such as ‘a’, ‘but’, etc.).

The motivation for the IDF_t is that the more wide spread the use of a token t is among all documents, the less likely it conveys information about the topic of any particular document. Hence, the more surprising a word is, the more likely it conveys information about the topic of the document in which it is found.

Thus, the TFIDF banks on both of these ideas and quantifies the important of a term for a given document.

Features regarding counts of the Reviews
- Word Count per Review
- Sentence Count per Review (Ren & Hong, 2017)

Sentiment Features
- The NRC sentiment score
  - Lists associations of words with eight emotions (anger, fear, anticipation, trust, surprise, sadness, joy, and disgust) and two sentiments (negative
    and positive)
- The Bing sentiment score
  - The bing lexicon categorizes words in a binary fashion into positive and negative categories.
- The Afinn sentiment score
  - The Afinn lexicon assignes words with a score between -5 and 5, where negative scores indicate a negative sentiment and positive scores indicate a
    positive sentiment.
    
Features of specific sentiment words
- Swear Words
  - Another valid linguistic correlate of sentiments is swearing (Hashimi, Hafez & Mathkour, 2015)
- Negation Words Feature
  - Negations are words like no, not, and never. When people want to express the opposite meaning of a particular word or sentence, this is done by
  inserting a specific negation. Negating words have a correlation with other words in that sentence and we assume they are useful for predicting the
  sentiments.
- Function Words (Functors) Feature T
  - These are words that have little lexical meaning or that have ambiguous meaning which express grammatical relationships among other words within a
  sentence, or specify the attitude or mood of the speaker. Therefore we assumed this to be a feature of use.
- Pronouns Feature
  - A pronoun is a word that takes the place of a noun. So words like: “I”, “me”, “he”, “she”, “herself”, “you”, “everybody” etc.
- Preposition Feature
  - These are words or a group of words that are used before a noun, pronoun, or noun phrase to show direction, time, place, location, spatial
  relationships, or to introduce an object. These are words like “in,” “at,” “on,” “of,” and “to etc. (Liang, Sun, Sun, & Gao, 2017)
  
<ins>Methods and Model employed:</ins> 

- Here Lasso and Ridge Regression were used. And they were compared based on their accuracy, sensitivity, and specificity.

<ins>Model Comparison</ins> 

- I decided to keep the Lasso Model, since it has the highest scores on both accuracy and sensitivity. Although ridge has a somewhat similar accuracy and a better specificity, the difference in sensitivity is much higher in favour of the lasso model. Thus, based on this analysis and the one before with the features and their weights I decided to use the lasso model.

<ins>Results:</ins> 

- The overall model accuracy employed on a test set was 85%.

<ins>References</ins>

Tan, C. M., Wang, Y. F., & Lee, C. D. (2002). The use of bigrams to enhance text categorization. Information Processing & Management, 38(4), 529–546. https://doi.org/10.1016/s0306-4573(01)00045-0

Hashimi, H., Hafez, A., & Mathkour, H. (2015). Selection criteria for text mining approaches. Computers in Human Behavior, 51, 729–733. https://doi.org/10.1016/j.chb.2014.10.062

Wu, S. T., Li, Y., & Xu, Y. (2006). Deploying Approaches for Pattern Refinement in Text Mining. Sixth International Conference on Data Mining (ICDM’06). Published. https://doi.org/10.1109/icdm.2006.50

Liang, H., Sun, X., Sun, Y., & Gao, Y. (2017). Text feature extraction based on deep learning: a review. EURASIP Journal on Wireless Communications and Networking, 2017(1). https://doi.org/10.1186/s13638-017-0993-1

Ren, G., & Hong, T. (2017). Investigating Online Destination Images Using a Topic-Based Sentiment Analysis Approach. Sustainability, 9(10), 1765. https://doi.org/10.3390/su9101765

Zhang, L., Hua, K., Wang, H., Qian, G., & Zhang, L. (2014). Sentiment Analysis on Reviews of Mobile Users. Procedia Computer Science, 34, 458–465. https://doi.org/10.1016/j.procs.2014.07.013


