## Parkinsons Vocal Analysis


### Project Overview
---
For this project, I have decided to focus on identifing patients being diagnosed with Parkinson’s disease based on their vocalization data. For context, Parkinson’s is a chronic neurodegenerative disorder that causes the degeneration of the brain, causing motor and cognitive issues that may lead to producing dysphonic voice due to probable neurogenic interruptions in the laryngeal nerve paths

Dysphonia is a phonation disorder with the difficulty in the voice production. Dysphonia can be observed with hoarse, harsh, or breathy vowel sounds, as a result of impaired ability of the vocal folds to properly vibrate during exhalation.
It is reported by Sewall et al that about 70% to 80% of IPD patients would suffer from dysphonia or other phonatory disorders, with the symptoms of decreased variation, roughness, increased asthenia, dysarthria, or voice tremor. The neurological dysfunction and debilitated communicative deficits of IPD patients greatly cause impact on their social communications and quality of life. Thus it is well within reason to assume a correlation between a patient’s ability to speak and their progression into Parkinson’s as these capabilities regress.

I will be working with a dataset obtained through a 2008 study by the journal, IEEE Transactions on Biomedical Engineering, of how various parameters of voice frequency can help classify if a patient is suffering from Parkinson’s. Through classification on this data, I hope to obtain findings that vocalization tests are indeed a well suited method to diagnose a patient for this disease.


### Problem Statement
---
This project attempts to prove that vocalization data from a patient can help diagnose whether or not they suffer from Parkinson’s. As such, it is initially assumed that there is a relationship between the two. I will attempt to run various machine learning classifiers (Ex. Naïve Bayes, SVM, etc.) on the data in hopes to reach a high predictability rate that is matched with a reasonable runtime. The study itself obtained a predictability rate of 91.4% and so I hope to reach a rate close to this or possibly to surpass it. If I can reach a rate that is within a 5% interval of the one obtained in the study, I will have proved the study correct.

The study first focuses on the linear correlations between 22 voice parameters of fundamental frequency variability, amplitude variations, and nonlinear measures. Then these highly correlated vocal parameters are combined by using the linear discriminant analysis method which I have carried forward in analysising in my code as well.


### Exploratory Visualization
---
To get a better grasp of the data, I developed a scatter matrix that allows me to see the relationship between the features presented from the data set. There are multiple correlations seen in the matrix, but I specifically analyzed the distribution of a feature when compared to the status of the patient. I noticed that across all features, those diagnosed with Parkinson’s had a larger spread of data than those who did not. While healthy patients had their data clustered near 0, the Parkinson patients had the features run across the entire axis. This results in a separation between the status of 1 and 0 in the spread1, spread 2, D2, and PPE columns. This division will allow for greater success by SVM classification, which can better separate the data with the hyper plane.

![Scatter](https://github.com/RadheV/Parkinsons-Vocal-Analysis/blob/master/scatter.png)

### Algorithms and Techniques
---
I have implemented multiple supervised learning algorithms to analyze the data set. My hopes are to find the classifier that is most optimal for this problem. Afterwards, I will be able to tune it to optimize its performance. The end goal is to optimize a model off of one of these classifiers so that it can perform as well or better than the predictability rate of those who wrote the study. I have chosen three different supervised classifiers as listed below:

Naïve Bayes: A classifier that makes use of Baye’s theorem to try and classify data. The use of Baye’s equation makes use of the likelihood of a specific classification based on probabilities returned from the features of the data. I decided to implement this classifier as it is known to only require a small training set to estimate parameters and is not sensitive to irrelevant features.

Support Vector Machines: A classifier that categorizes the data set by setting an optimal hyper plane between data. I chose this classifier as it is incredibly versatile in the number of different kernelling functions that can be applied. I hopes are that when tuned, this model can yield a high predictability rate.

Stochastic Gradient Descent: A classifier that applies the concept of gradient descent to reach an optimal predication rate. I chose this classifier because it has multiple parameters that could potentially be tuned if it produces strong results under my data set. My main concern is that it tends to work well with sparse data, but is sensitive to larger training sets.

Gradient Tree Boosting: An ensemble classifier (combines predictions of base estimators) that makes use of multiple decision trees - giving their contributions weights – to classify data. The weights are developed using the gradient descent algorithm. I decided to implement the GTB because of its strength in handling heterogeneous features and high accuracy. The problem I do expect with this classifier is that it scales poorly and so with larger sets of data, this would not be optimal. It is still interesting to see the results of this classifier however.


### Benchmark
---
The benchmark for this project is the resulting prediction rate from the original study. I expect to obtain a predictability rating that is at least 5% within the margin of the 91.4% they obtained in their analysis to be successful.


### Data Preprocessing
---
There was no need to implement feature transformation, as all of the data is continuous. The data itself does not project any outliers that I feel would have an enormous impact on the classifiers I have created. Thus no effort has been made to seek out and eliminate data points.


### Implementation
---
The supervised learning algorithms ran smoothly with the given data set. I encountered no issues with the metrics and techniques I applied. Some effort was made to tinker with the scatter matrix I produced so that the labels were clearly visible. I should report that I have created multiple functions to help in the training and prediction from my classifiers. This makes it relatively easy to do so for multiple classifiers as I am.


### Refinement 
---
I successfully produce F1 scores based off the predictions made by my classifiers. Below I have listed the results in a table (NOTE: Time is in seconds):

|     | Naive Bayes |     SVM     |     SGD     |     GBT     |
|-----|-------------|-------------|-------------|-------------|
| 50  |    0.7619   |    0.9268   |    0.8947   |    1.0000   |
| 100 |    0.7833   |    0.8820   |    0.5047   |    1.0000   |
| 150 |    0.7568   |    0.8933   |      0      |    1.0000   |


Graphing the the F1 scores of the four classifiers I have tested, I've eliminated Gradient Boosting as the score is perfect consistently for all there sets of data showing that it overfits extremely well on the training data and thus low variabiltity in its aspect. The classifier will underperform completely on an unseen test data and therefore deemed as unsuitable.

I have also elimated SGD classifier as it is better when data is sparse (ex. Text classification), but is sensitive otherwise as shown that the f1 score is 0.0 as the training data increases to 150.

Between both my viable choices of Naives Bayes and SVC which have both high and most consistence in their F1 score, Support Vector Machines is the most suitable choice with a higher f1 score throughout the 50,100 and 150 training data increment.


### Model Evaluation and Validation
---
The final model aligns with the solution expectations. It produces a F1 score under the best parameters from tuning. I have tested the model under unseen data I have created and it works successfully. The SVM classifier itself is inherently robust to small changes in the training data. We can trust the results from the model, but in industry it may not be so. This is because the final accuracy rate of the SVM was 87.67%, which has a large error for the healthcare industry. Most diagnosis methods must be 97% accurate for them to be applied on patients.


### Justification
---
The final results are not as strong as the benchmark provided by the study of 91.4%. My model’s final rate was 89.74%. However, this does verify the study as my model is within a 5% margin of their analysis. I believe with even further scrutiny in the tuning of the model, I may be able to achieve the same result as that with the study. It may be possible to achieve even a higher rate but that would require a very thorough optimization of the parameters and cleaning of the data for small outliers.


### Improvement
---
The model itself can be further tuned to try and improve the prediction rate. I was able to figure out how to use all the algorithms I implemented, but I know that more supervised learning classifiers exist and they have potential in classifying this data. As for my final solution, I believe a better solution exists with more time implemented to optimizing the parameters of the classifier and analyzing more supervised classifiers. A classifier that is created for specifically this type of problem could perform the best.


### Future Recommendation
---

The proposed diagnosis method could be valuble as an additional method to reconfirm the diagnosis of Parkinson’s disease and perhaps mainfested into other variations of testing of speech and language deficiencies.


### References
---

[1]. Sewall G. K., Jiang J., Ford C. N. Clinical evaluation of Parkinson's-related dysphonia. Laryngoscope. 2006;116(10):1740–1744. doi: 10.1097/01.mlg.0000232537.58310.22. [PubMed] [CrossRef] [Google Scholar]

[2]. Bhuta T., Patrick L., Garnett J. D. Perceptual evaluation of voice quality and its correlation with acoustic measurements. Journal of Voice. 2004;18(3):299–304. doi: 10.1016/j.jvoice.2003.12.004. [PubMed] [CrossRef] [Google Scholar]
