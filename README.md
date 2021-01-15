# seedcode-DS-trial

The data contains 134 features for one target binary variable.  

The goal is to build a binary classifier that can classify that the given clinical trial will succeed or not. This has to be done with  positive prediction value (PPV) of 90% while maintaining a healthy detection rate (DR).  

## Installation:  
To run this notebook
1. Download this repository in a zip file by clicking on this link or execute this from the terminal git clone https://github.com/ali-08/seedcode-DS-trial.git
1. Install ![virtualenv](http://virtualenv.readthedocs.org/en/latest/installation.html).  
1. Navigate to the directory where you unzipped or cloned the repo and create a virtual environment with ````virtualenv env````.
1. Activate the environment with source env/bin/activate.  
1. Install the required dependencies with ````pip install -r requirements.txt````.
1. Comment out the first cell if not using colab.
1. Execute ipython notebook from the command line or terminal.
1. Click on seedcodeTrialFinal.ipynb on the IPython Notebook to get the results or seedcodeTrialWorking.ipynb to see the working.

#### Dependencies:
* [NumPy](http://www.numpy.org/)
* [IPython](http://ipython.org/)
* [Pandas](http://pandas.pydata.org/)
* [Scikit-Learn](http://scikit-learn.org/stable/)
* [Matplotlib](http://matplotlib.org/)

### Goal of this task
* To build a classifier with a good accuracy (assumed to be 80%+)
* To get the PPV (precision) of 90%.

### Data Pre-processing
There are 38 numerical variables and 96 categorical variables. There was difficulty in gaining the insights from data as the variable names were hidden due to the sensitive nature of data.  
The missing values of numerical data were replaced by mean whereas the missing values of categorical data were dropped since other methods of dealing with them results in a drop of accuracy by 5-9%. This was by far the best method to boost the performance of the model for this dataset.
Categorical missing values were replaced by modal ones, but failed to increase the performance.
Feauture Reduction was also carried, by dropping the variables that had either too many missing values or the dropping the ones with poor results of statistical testing. However, it also resulted in the reduction of performance metrics. 
Feature Selection methods like chi-squared statistic and the mutual information statistic were also used but failed to show any significance in feature importance, thus they were not taken into consideration.  
PCA was also applied, capturing upto 75-80% of variance, but also failed to improve the perfomance.

## Model fitting
A number of classification models were applied including:
- Logistic Regression
- KNN classifier
- SVC
- Multi-layer Perceptron
- Random Forest
- Ada Boost  
Random Forest provided the best results, closely followed by Multi-layer perceptron and Ada Boost. This could be due to the fact that these models have in built feature selection mechanism. In random forest, each feature decreases the impurity, which helps to determine the importance of each variable.

### Train-test split
Stratified k-fold of sklearn was used to ensure that the training and testing samples have equal propotion of data points of each class.

### Performance Metrics
Since the task required the precision to be 90% without comprising accuracy, the recall has to sacrificed due to precision recall tradeoff. This can be measured using the F1-score, which is simply the harmonic mean of precision and recall. Random forest provided the best results based on this evaluation criterion.

### Classification Threshold
For predicting a diseases i.e. 1 as the class label, the **threshold value of 81** was used. This means the the probability of class 1 of predicted output should be greater than 0.81. UNKNOWN lie in the range of 0.69 - 0.80.

## Results  
Following results were achieved on test set:
- ```PPV: 90.59%```
- ```Accuracy: 81.04%```
- ```f1-score: 0.65```
