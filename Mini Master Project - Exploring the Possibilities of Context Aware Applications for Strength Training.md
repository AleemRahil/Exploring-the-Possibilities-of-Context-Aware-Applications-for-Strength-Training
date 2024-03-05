Exploring the Possibilities of Context-Aware

Applications for Strength Training


Abstract. Strength training, in addition to aerobic exercises, is an im- portant component of a balanced exercise program. However, mecha- nisms for automatically tracking free weight exercises have not yet been fully studied. The aim of this paper is to further explore the possibili- ties of context-aware applications within the strength training domain. It does so by analyzing wristband accelerometer and gyroscope data ob- tained during strength training sessions. The collected dataset contains data of 5 participants performing various barbell exercises. The goal is to explore, build, and evaluate models that can, just like human personal trainers, track exercises, count repetitions, and detect improper form. The methods evaluated in this paper use a supervised learning approach for classication. Various machine learning algorithms were trained using the collected dataset and accuracies were compared to nd and evaluate the right models.

1  Introduction

During the last decade, many practical constraints related to carry-on sensors like accelerometers, gyroscopes and GPS-receivers have been solved. This has en- abled monitoring and classication of human activity based on information from wearables such as smartwatches to become a growing research area of pattern recognition and machine learning. The grounds for that lie in high commercial potential of context-aware applications and user interfaces. Moreover, activity recognition can be utilized to attack some of the serious societal challenges like rehabilitation, sustainability, elderly care and health.

To promote healthier lifestyles, works from the past have focused on tracking movements and user feedback via exercise management systems. Such systems partly replace tasks that are currently fullled by personal trainers. For example, in the category of aerobic exercises such as bicycling, swimming, and running, there are accelerometer and GPS-based pedometers to track running pace and distance, ECG monitors to track exertion, and electronic exercise machines such as treadmills, elliptical trainers, stair climbers, and stationary bikes. Weight training, in addition to aerobic exercises, is an important component of a bal- anced exercise program [1]. However, mechanisms for tracking free weight exer- cises have not yet been fully studied. Currently there is only one tness wearable brand on the market that claims to automatically identify exercises and record repetitions [4]. However, the available literature on context-aware applications

Context-Aware Applications for Strength Training 7

within the strength training domain is still limited which is probably due to the commercial potential in such methods.

With advancements in context-aware applications, it should eventually be possible to create fully digital personal trainers. To establish the requirements of such a digital trainer, the roles of current personal trainers will be discussed briey. First of all personal trainers must have knowledge of human anatomy and fundamental principles of exercise science and nutrition. Secondly, the ability to design and execute exercise programs, tailored to the needs and attainable goals of the individual in an eective and motivational way. Finally, a way of tracking workouts to ensure appropriate form, and progressive overload is applied to exercises in order to help clients safely reach their tness goals [5].

While recent years have seen great improvements on digitalizing the rst two roles of the personal trainer, the nal, and most important role in terms of safety and progress, is not well implemented in today's tness wearables and applica- tions yet. Therefore, the aim of this paper is to further explore the possibilities of context-aware applications within the strength training domain. It does so by analyzing wristband accelerometer and gyroscope data obtained during free weight workouts. The collected dataset contains data of 5 participants perform- ing various barbell exercises with a medium to heavy weight. The goal is to explore, build, and evaluate models that can, just like human personal trainers, track exercises, count repetitions, and detect improper form. The methods evalu- ated in this paper are based on work from Hoogendoorn and Funkuse [2] and use supervised learning approaches for classication. Various machine learning algo- rithms were trained using the collected dataset and accuracies were compared to nd the right models.

The structure of this paper is as follows. Section 2 discusses related work. In Section 3 the method for collecting the data is explained followed by the process of converting the raw data in section 4. Section 5 will explain how additional features were extracted from the data and section 6 will explain how the models were built and evaluated. Finally section 7 highlights the conclusion.

2  Related Work

The rst work on activity recognition using wearable sensors was published in 2000 by Van Laerhoven [7]. For their study they connected a pair of pants with accelerometers to a laptop to interpret the raw sensor data collected during daily activities. Using a combination of machine learning techniques such as Kohonen maps and probabilistic models, a system was build that was able to recognize activities. Recognizing daily activities is still one of the most studied problems in the area (e.g. [8], [9], [10], [11]). The results of those studies are nowadays widely deployed and implemented in various commercial products like Fitbit [13], Apple Watch [15], and Samsung Gear [14]. Furthermore, smartphones are currently equipped with features to track typical tness activities like walking, running, and cycling provided by Google [16] and Apple [17]. More recent devices and application even support recognition of more sport specic activities like

aerobic workouts, elliptical training, and swimming. Fitbit's SmartTrack feature automatically recognizes and records workouts and captures stats like: activity duration, calories burned, and heart rate zones [18]. These products already promote the idea of a digital personal trainer, however there is still lack of support for free weight exercises.

There are studies that focused on recognizing gym exercises through wear- able sensor data like [19], [21] and [20]. Chang et al. incorporated a three-axis accelerometer into a workout glove to track hand movements and put another accelerometer on a users waist to track body posture. Data was collected by asking 10 dierent subjects to perform 3 sets of 15 repetitions for nine dierent exercises with various weights. To recognize the exercises, two methods were eval- uated: Nave Bayes Classier and Hidden Markov Models which both achieved an overall recognition accuracy of around 90% based on single user data, and the accuracy was around 85% when cross-validating training results with new user data. In order to count repetitions, a peak counting algorithm was developed which achieved around a 5% miscount rate.

Koskimki et al. [21] discussed that one of the limitation of previous work was the lack of exercise variety. In this study, two accelerometers were used, one on the left wrist and another on the torso. The aim was to create automatic activity diaries showing reliably to end users how many sets of given exercise have been performed. The data was collected from a single person from 30 dierent exercises, each of them consisting of 3 sets of 10 repetitions. This process was repeated: the rst set for training and the second for independent testing. The person specic model could recognize the exercises with an on average 96% true positive rate. However, when using a separate validation test set, the accuracies decreased signicantly for some classes.

Li et al. [19] presented a new recognition method based on one accelerometer attached to a glove, in which a ltered acceleration data stream was divided into time series with unequal lengths for peak analysis instead of conventional xed length windows. Based on this time series, Dynamic Time Warping was deployed to recognize exercises. The experiments were conducted by three male and a female subjects. Every subject did each exercise in 3 sets using dierent weights. They were told to try their best to 15 repetitions in each set. Their results show that the proposed approach is feasible and can achieve good performance.

The results achieved in these studies are very promising and it shows that exercise recognition through accelerometer data is feasible. However, from a pure strength training and bodybuilding perspective, the works ignored some of the key aspects of weight training, namely progressive overload and correct form. Progressive overload is the gradual increase of stress placed upon the body during exercise training and is recognized as a fundamental principle for success in various forms of strength training programs [23]. Progressive overload can be applied by either increasing the weights or repetitions over time. While previous work mentioned using various weights, the weights were not proportional to the repetitions as in all cases the subjects were instructed to try and do the same amount of repetitions regardless of the weight. All sets were executed with either 10 or 15 repetitions which is high from a strength training perspective where typical sets usually do not exceed 5 repetitions [24]. This means that all of the weights used in these studies can still be considered light, in case of the 15 reps, and medium at most in case of the 10 reps. Moreover, none of these studies mention anything about the perceived intensity of the exercises. If the goal is to create a context aware application that can be used during workouts, then training data should resemble a realistic workout scenario. Furthermore, none of the studies examine the quality of execution of the exercises which is an important aspect of free weight training, and an essential feature of a digital personal trainer, as improper form can lead to serious injuries, especially when using heavier weights.

3  Experimental Setup

Other works have shown that it is feasible to apply various machine learning algorithms to free weight exercise accelerometer data and achieve great results. However, from a strength training perspective, the process of collecting quality datasets has been neglected. This study tries to solve that by setting up an experimental environment that mimics real strength training workouts.

Related works seem to have chosen random sets of exercises. There is no motivation as to why the specic exercises were chosen for the dataset. While it is important to capture a wide variety of exercises, this study will focus on the exercises from one specic training program. This ensures that there is no noise from certain exercise combinations that one would never perform together in a real workout scenario. The program Starting Strength, by Mark Rippetoe, is considered to be the fundamental strength training program that can ben-

et beginners as well as experienced lifters to become stronger [24]. Starting Strength makes use of basic barbell exercises that involve all muscles, utilized over the longest eective range of motion and loaded progressively, to force the adaptations necessary for increased strength [24]. The program is made up of 5 fundamental barbell exercises: Bench Press, Deadlift, Overhead Press, Row, and Squat. The exercises are shown in Figure 1.

![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.001.png)

Fig.1. Basic Barbell Exercises

In strength training, a program is described using the terms sets and repetitions (reps). A rep is one complete motion of an exercise and a set is a group of consec- utive repetitions followed by a resting period. In the Starting Strength program, exercises are performed with a heavy weight. The aim is to pick a weight so that around 5 repetitions can be done. This weight is relatively much heavier than the weights used in others works and should change the execution in terms of bar path and speed compared to lighter weights. It should be examined whether

a trained model can still correctly classify exercises given these dierences. Fur- thermore, possible ways of checking the form of an exercise should be explored.

1. Data Collection

While other works focused solely on accelerometer data, most current smart devices contain more carry-on sensors, like a gyroscope, which could provide additional information. Moreover, the sensors were placed in strange places like a band around the torso or a workout glove. If the goal is to create a commercial product out of these ndings, then it should be implemented in something more practical, like a smartwatch, which already contains all of the required sensors. Therefore, MbientLab's wristband sensor research kit [12] was used to collect data for this experiment. The wristband mimics the placement and orientation of a watch while allowing for controlled experiments. Data was collected using the default settings of the sensors: accelerometer: 12.500HZ and gyroscope: 25.000Hz. In order to collect a representative dataset, 5 participants (Table 1) were asked to perform the barbell exercises in 3 sets of 5 repetitions. Just as in the Starting Strength program. In another training session, the participants were asked to perform the same exercises but in 3 sets 10. These sets of higher reps will be used to see how models generalize over dierent weights. This resulted in a total of 150 (5x5x6) sets of data. Additionally, in between some sets 'resting' data was collected. To keep the data as representative as possible, the test subjects had no restrictions during the resting periods. Therefore, the resting periods are

a mix of standing, walking, and sitting. This data will be used to examine the state change from rest to exercise.

2. Weights

To determine the appropriate weight, the one rep max (1RM) metric was used. The 1RM is the maximum amount of weight that a person can possibly lift for one repetition [27]. 1RM can either be calculated directly using maximal testing or indirectly using submaximal estimation. The latter method is preferred as it is safer and quicker. There are several common formulas used to estimate 1RM using the submaximal method, the Epley and the Brzycki being the most common [26]. For this experiment Epley's formula was used:

r 1RM = w(1 + ) 30

Where r is the number of repetitions performed and w is the amount of weight used. After calculating the 1RM for each exercise, Epley's formula can also be used to calculate the weight for 5 or 10 reps. This is around 85% (5 reps) and 75% (10 reps) of the 1RM. This method ensures that all participants perform the exercises with weights relative to their strength in the most accurate way.

Table 1. Participants (N=5) Participant![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.002.png) Gender Age Weight (Kg) Height (cm) Experience (years)![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.003.png)

A Male 23 95 194 5+ B Male 24 76 183 5+ C Male 16 65 181 <1 D Male 21 85 197 3 E Female 20 58 165 1![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.004.png)

3. Execution Form

Next to the main dataset, additional data was collected in order to examine the quality of execution (i.e. form) of an exercise. For now, this was only done for the bench press. A participant was asked to purposely execute the bench press movement with improper form. The data includes two of the most common errors for this exercise: lowering the bar too high on the chest and not touching the chest at all [28].

4  Converting Raw Data

The raw dataset contained a total of 69677 entries, each containing an epoch timestamp and x, y, and z-values from the sensor. The individual sensor mea- surements from the wristband are split up into dierent les where each entry

has a unique timestamp. Because of this, the data had to be aggregated. To minimize information loss in this process, a small step size of t = 0.20 s, i.e. ve instances per second was chosen. Numerical values were aggregated using

the mean, and categorical attributes (labels) were aggregated using the mode. The aggregated dataset provided us with a good starting point for visualizations. Figure 2 shows accelerometer data for a heavy set of each exercise. The gure shows that exercise patterns are pretty unique and the repetitions can easily be identied from the peaks. Figure 3 shows the dierences in y-acceleration be- tween medium and heavy squat sets. The medium weight sets have higher peaks whereas the heavy sets have deeper drops. This makes sense as medium weight reps go up faster due to lower resistance while the heavy reps drop down faster due to the heavy load.

This section will continue to explain approaches for handling raw, noisy data. The goal is to transform the data in a way that subtle noise is ltered and the

![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.005.png)

Fig.2. Accelerometer Data

parts of our data that explain most of the variance are identied. Two ap- proaches will be discussed: Low-pass Filtering, which can be applied to individ- ual attributes, and Principal Component Analysis, which works across the entire dataset.

![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.006.png)

Fig.3. Medium and heavy weight squats

1. Low-pass Filter

The low-pass lter can be applied to data that is of temporal nature, and assumes that there is a form of periodicity. The Butterworth low-pass lter can remove some of the high frequency noise in the dataset that might disturb the learning process [2]. The lter was applied to all but the target features. The visualizations showed that the movements have a frequency of around 2 seconds per repetition. After some further visual inspection of some trial-and-error results as suggested in the work of van den Bogert [3], the cut-o point was set at 1.3 Hz. Figure 4 shows the y-acceleration for a heavy bench press set before and after smoothing.

![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.007.png)

Fig.4. Low-pass Filter and Principal Component Number

2. Principal Component Analysis

A principal component analysis (PCA) was conducted to nd the features that could explain most of the variance. PCA was applied to all features excluding the target columns. The results are visualized in Figure 4 which shows that the explained variance drastically decreases after 3 components. Therefore, 3 components are selected and their values are included into the dataset.

5  Feature Engineering

This section we will discuss how additional features were derived from the orig- inal dataset including aggregated features, time features, frequency features, and clusters.

1. Aggregated Features

To further exploit the data, the scalar magnitudes r of the accelerometer and gyroscope were calculated. r is the scalar magnitude of the three combined data points: x, y, and z. The advantage of using r versus any particular data direction is that it is impartial to device orientation and can handle dynamic re-orientations [29]. r is calculated by:

p ![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.008.png)

rmagnitude = x2 + y2 + z2

2. Time Domain

To exploit the temporal nature of the data, numerical data points were aggre- gated by taking the standard deviation (sd) and the mean of all features except

Context-Aware Applications for Strength Training 9

the target columns over various window sizes. The sd should capture the varia- tion in the data over time. For example, the sd is expected to be higher during exercises than during resting periods. The temporal mean will indicate more about the general levels of the data, with less inuence from spiky noise. When selecting an appropriate window size, one should balance how strongly the data would be aected by noise on the one hand, and maintaining predictive power on the other hand. Figure 5 shows the results for windows sizes of 2, 4, and 6 seconds. A windows size of 4 seconds was chosen and added to the dataset.

![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.009.png)

Fig.5. Numerical temporal aggregation with window sizes of 2, 4, and 6 seconds

3. Frequency Domain: Fourier Transformation

Besides the time domain, the frequency domain will also be explored. The idea of a Fourier transformation is that any sequence of measurements can be rep- resented by a combination of sinusoid functions with dierent frequencies [2]. The same window size of 4 seconds was used to compute the frequency features with a Fourier Transformation including the maximum frequency, the frequency signal weighted average, and the power spectral entropy [2].

4. New dataset

The dataset now contains various new features. However, since there are over- lapping time windows, the resulting attributes are highly correlated. Given this overlap, just including all instances might not provide us with new information as only one point in the window diers for adjacent instances. To prevent overt- ting, a maximum overlap for the windows was set and accordingly instances for which this criterion is not met were removed. 50% overlap was allowed for. This reduced the dataset to 4505 instances. Some information is lost in this process but it has been shown to pay o as there are less very similar instances in the dataset that could cause overtting [2].

5. Clustering

It is possible that a membership to a certain cluster can help predict a label. The focus will be on clustering the acceleration data as the results showed that the gyroscope data was not useful. After running some tests, k-means clustering (k=4) was the preferred method as it resulted in the best silhouette score (0.6478) compared to other possible methods (k-mediods & agglomaritive clustering). 4 cluster were chosen as this captured the dierent labels in the best way despite having a little higher silhouette score for k=2. The results are shown in Figure 6. Table 2 shows the distribution of the measurements and labels. Cluster 1 covers almost all the bench press and overhead press data. This makes sense as both pressing movements are very similar. The squat is captured in cluster 2 and the deadlift and row are captured in cluster 3 with a perfect score. Cluster 4 contains some of the rest data but fails to capture this accurately.

![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.010.png)

Fig.6. Clusters

Context-Aware Applications for Strength Training 11

Table 2. Cluster Coverage



|Label|Cluster 1 Cluster 2 Cluster 3 Cluster 4|||
| - | - | :- | :- |
|BenchPress|99\.88 %|0\.12 % 0.00 %|0\.00 %|
|Deadlift|0\.00 %|0\.00 % 100.00 %|0\.00 %|
|OHP|99\.28 %|0\.72 % 0.00 %|0\.00 %|
|Row|0\.00 %|0\.00 % 100.00 %|0\.00 %|
|Squat|2\.98 %|97\.02 % 0.00 %|0\.00 %|
|Rest|4\.14 %|3\.78 % 50.45 %|41\.62 %|

6  Modeling

The dataset is now processed and ready for training. The dataset contains the 6 basic features, 2 scalar magnitude features, 3 PCA features, 16 time features, 12 frequency features and 1 cluster feature. This section will explain how the models for classication, repetition counting, and form detection were built and evaluated.

1. Classication

Because of the temporal nature of our dataset, the training and test set were split up based on the exercise sets. The training data contains the rst two sets for each exercise, weight, and participant combination and the test set the remaining sets. This ensures that we have valid test data of sets the models have not seen before.

Feature selection Forward feature selection was used to investigate which features contribute the most to performance as useless features could impact the performance of the algorithms. Using a simple decision tree, and gradually adding the best features, the results showed us that after 15 features the perfor- mance no longer signicantly improved. The 5 features with the most predictive power are: pca~~ 1 , acc~~ y, pca~~ 3 , gyr~~ x~~ temp~~ std~~ ws~~ 4 , acc~~ r~~ pse .

Regularization In order to punish more complex models, a regularizer was added to the objective functions. Figure 7 shows the impact of adding a regu- larization parameter on the performance for the training set. It shows that the accuracy of the test set slightly improves with a higher regularization parameter, but only until a certain point. After that, the accuracy decreases on both the training and the test set.

Models First, an initial test run was done to determine the performance of a selection of models and features. This test included the following models: Neu- ral network, Random Forest, Support Vector Machine, K-nearest Neighbours, Decision Tree, Naive Bayes. Grid search was performed on all of the models.

![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.011.png)

Fig.7. Regularization

2. Classication Results

The results per model can be seen on the left in gure 8. The colors represent the dierent feature sets as explained in [2]. The chapter 5 feature set contains all features. Based on these results a Random Forest was further optimized with the 15 best performing features. Using a 5-fold cross validation upon which grid search parameter tuning was performed, the following optimal parameters for the Random Forest were found: minimum samples per leaf: 2, n-estimators: 100, criterion: gini. A confusion matrix of the nal predictions is shown on the right in Figure 8. The model achieved an overall accuracy of 98.51% with a similar precision, recall and f1-score on the test set.

![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.012.png)

Context-Aware Applications for Strength Training 

Fig.8. Model Performance and RF Classication

3. Counting Repetitions

Confusion Matrix

Context-Aware Applications for Strength Training 

To count repetitions, a simple peak counting algorithm was applied to the scalar magnitude acceleration data. To make sure small local peaks were neglected, a strong low-pass lter with a cut-o at 0.4 Hz was applied rst. It was found that this method of counting repetitions has to be adjusted to the individual exercises for the best performance. For the deadlift and overhead press, better results were obtained by counting minimum values. The overall error rate for

Context-Aware Applications for Strength Training 15

counting repetitions was about 5% for the collected dataset. An example of 10 deadlift repetitions is shown in Figure 9.

![](Aspose.Words.23813408-fcb0-49f5-8900-1a530f7efda0.013.png)

Fig.9. Counting deadlift repetitions using the minimum values after applying a low- pass lter

4. Detecting Improper Form

During the experiments additional data was collected from one participant per- forming the bench press with improper form. The participant performed a couple of sets where the bar was purposely placed too high on the chest or did not touch the chest at all. This data was then used to train a Random Forest, similar to the one explained in this section, to classify the form. The data contained three labels: correct form, too high, and no touch. The same method of training and testing as explained earlier was applied to the dataset consisting of 1098 in- stances. The model achieved an accuracy of 98.53% on the test set.

5. Generalization

It is important to evaluate how the models generalize to new data. Lets rst consider the dierent weight classes. Figure 3 in section 4 already showed that there are pace dierences between the two classes. To examine these dierences, the data was split up in to a training and testing set based on the weight class. When training on the heavy data, the model fails to properly generalize to the medium weight sets. In this case the accuracy drops to 79.97%. The other way around results in a similar accuracy of 79.51%. Lets now consider the dierent participants. Here the leave one out method was applied for training and testing which resulted in an average accuracy of 85.43% over all the participants.

7  Conclusions

This paper aimed to explore the possibilities of context-aware applications within the strength training domain. The motivation for this research was the lack of focus on strength programs in the related literature and support from current activity trackers.

Wristband accelerometer and gyroscope sensor data was collected during real strength training sessions of 5 participants performing the ve basic barbell lifts with medium and heavy weights. The 1RM metric was used to ensure partic- ipants were performing the lifts with weights relative to their strength. After applying the machine learning for the quantied self cycle [2] to the data, a Random Forest turned out to be the best exercise classication model. The model achieved an overall accuracy of 98.51% on classifying unseen instances. To account for a possible accuracy paradox, the precision, recall and f1-score were also evaluated and showed that the results are sound. The model could not achieve a perfect score because it wrongly classied some bench press instances as overhead press and the other way around. The same goes for the deadlift and row. A possible explanation for this is that both the bench press and overhead press are vertical pressing movements. While the torso is in a dierent position, the wrist orientation is similar. The same holds for the deadlift and row as both are vertical pulling movements. A simple peak counting algorithm, in combina- tion with a strong low-pass lter, was applied to the data to count repetitions. It was found that, in order to achieve the best results, rep counting models should be tweaked per exercise. While the method is very basic, it achieved decent re- sults with a miscount rate of 5%. Another Random Forest was trained to classify bench press form. Data was collected from one participant purposely performing the bench press with bad form. The Random Forest was able to classify the cor- rect instances from the improper ones with an accuracy of 98.53%. Although the form detection data is limited, and future work should examine other exercises, the proposed method can serve as a proof of concept.

While these results show great promises for possible commercial applications, some tests showed that the models have some problems generalizing to new data. Therefore, in order to realize such systems, lots of training data from a variety of sources is required. With that in mind, we are on our way to create fully digital personal trainers, available from our wrists, that can help us obtain our health, tness, and strength training goals.

References

1. The Presidents Council on Physical Fitness and Sports. Fitness fundamentals guidelines for personal exercise programs. online council publications (2003), https://www.hhs.gov/tness/index.html
1. Hoogendoorn, M., & Funk, B. Machine Learning for the Quantied Self.
1. Van Den Bogert, M. (1996). Practical Guide to Data Smoothing and Filtering.
1. Atlas Wristband 2, https://atlaswearables.com/
5. American College of Sports Medicine. (2013). ACSM's Resources for the Personal Trainer. Lippincott Williams Wilkins.
5. Read, R. Kasparian, M. Li, P. 2015, USD725512S1, https://patents.google.com/patent/USD725512S1
5. Van Laerhoven, K., & Cakmakci, O. (2000, October). What shall we teach our pants?. In Wearable Computers, The Fourth International Symposium on (pp. 77-

   83. IEEE.
5. Ermes, M., Prkk, J., Mntyjrvi, J., & Korhonen, I. (2008). Detection of daily activities and sports with wearable sensors in controlled and uncontrolled conditions. IEEE transactions on information technology in biomedicine, 12(1), 20-26.
5. Banos, O., Damas, M., Pomares, H., Prieto, A., & Rojas, I. (2012). Daily living

activity recognition based on statistical feature quality group selection. Expert Sys-

tems with Applications, 39(9), 8013-8021.

10. Zhang, M., & Sawchuk, A. A. (2013). Human daily activity recognition with sparse representation using wearable sensors. IEEE journal of Biomedical and Health In- formatics, 17(3), 553-560.
10. Leutheuser, H., Schuldhaus, D., & Eskoer, B. M. (2013). Hierarchical, multi- sensor based classication of daily life activities: comparison with state-of-the-art algorithms using a benchmark dataset. PloS one, 8(10), e75196.
10. MbientLab, https://mbientlab.com/
10. Fitbit, https://www.tbit.com/
10. Samsung Gear, https://www.samsung.com/us/mobile/wearables/
10. Apple Watch, https://www.apple.com/lae/apple-watch-series-4/
10. Location API, https://developers.google.com/location-context/"
10. MotionActivity, https://developer.apple.com/documentation/coremotion/cmmotionactivity"
10. Fitbit Smarttrack, "https://www.tbit.com/nl/smarttrack"
10. Li, C., Fei, M., Hu, H., & Qi, Z. (2012, September). Free weight exercises recog- nition based on dynamic time warping of acceleration data. In International Con-

    ference on Intelligent Computing for Sustainable Energy and Environment (pp.

    178-185). Springer, Berlin, Heidelberg.

20. Chang, K. H., Chen, M. Y., & Canny, J. (2007, September). Tracking free- weight exercises. In International Conference on Ubiquitous Computing (pp. 19-37). Springer, Berlin, Heidelberg.
20. Koskimki, H., & Siirtola, P. (2014, December). Recognizing gym exercises using acceleration data from wearable sensors. In CIDM (pp. 321-328).
20. Ward, J. A., Lukowicz, P., & Gellersen, H. W. (2011). Performance metrics for activity recognition. ACM Transactions on Intelligent Systems and Technology (TIST), 2(1), 6.
20. Kraemer, W. J., Ratamess, N. A., & French, D. N. (2002). Resistance training for health and performance. Current sports medicine reports, 1(3), 165-171.
20. Rippetoe, M., & Kilgore, L. (2007). Starting strength: Basic barbell training. Wi- chita Falls, Texas, USA: Aasgaard Company.
20. One rep max calculator, https://strengthlevel.com/one-rep-max-calculator
20. Wood, T. M., Maddalozzo, G. F., & Harter, R. A. (2002). Accuracy of seven equations for predicting 1-RM performance of apparently healthy, sedentary older adults. Measurement in physical education and exercise science, 6(2), 67-94.
20. Marchese, R., & Hill, A. (2011). The essential guide to tness: for the tness

    instructor. Pearson Australia.

28. Bench Press Mistakes, https://barbend.com/common-bench-press-mistakes/
28. Arfken, G., & Weber, H. J. Mathematical Methods for Physicists (Academic, San Diego, 1985). Google Scholar, 232-236.
