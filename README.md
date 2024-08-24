# Practical Application Assignment 17.1: Comparing Classifiers

Assignment 17.1 is a python project showing my ability to apply the full CRISP=DM framework while comparing the performance of the classifiers (k-nearest neighbors, logistic regression, decision trees, and support vector machines) you encountered in this section of the program.  


## Contact 
If you want to contact me you can reach me at contactbethford@gmail.com

  
  
## Files
* 17.1.ipynb - Main python script with full charting and data
* images/ModelPerformance.png
* images/PCA_Chart.png
* images/CorrelationHeatMap.png
* README.md


## Data
The dataset comes from the UCI Machine Learning repository Links to an external site. The data is from a Portuguese banking institution and is a collection of the results of multiple marketing campaigns. In an effort to use the data to determine who to best target for term deposits. While the job variable had 11 different values, I paired down to two variables based on income type: those with a steady income versus more variable types.  Additonally I mapped months, default, housing and loan to numericals.  I added a new field to account for not only how long a conversation was, but also how often they happened in order to account for the investment in total time. Variable potcome was dropped as we had too much missing data.  Additonally, I dropped the default variable as their were only 815 values, and people on default are too much of a business risk. 

## Methodology
I first looked to the correlations to the Y variable.  ![Picture of correlation of all variables.](/images/CorrelationHeatMap.png) I then transformed the categorical variables and then scaled the numericals. I rechecked correlations with transformations in place. 
I then ran a Lasso regression to see if there were significant non zero variables.  Without success, I first tried to run the different types of classifiers.  The svc classifier would not run to completion on my computer.  I knew that I still needed to reduce the variables.  To that end, I moved on to a principal component analysis with 2 components.  ![Picture of PCA Components.](/images/PCA_Chart.png) Based on these results, I was able to create a reduced testing sets based on the top features. 



**Modeling:**
- 45,211 records
- Variables - Top Features, ['age','duration', 'totalTime', 'marital_single', 'marital_married', 'y']
- I ran five different classifier models (LogisticRegression(2), DecionTrees, KNearestNeighbor, SupportVectorMachines )
- I ran cross validation on the strongest model of SVM, which validated the accuaracy scoresa 
- With the recall and precision at 0, I realized that I needed to weight the classes to make them more balanced.  With this method, the recall and precision rose.
- I then tested out different types of kernels with sigmoid and rbf, but linear stayed with the highest accuracy.  


**Overall Findings**
- While Decisions Trees had the highest accuracy at .886, the F1 score is twice as high with the Support Vector Machine using linear kernels as we want to take a balanced approach to predict who will book a term of deposit.  Recall is not as import as I have reduced the risk in removing the default records. 

![Picture of a bar chart showing linear SVM is the best choice.](/images/ModelPerformance.png)



## Recommendations
- 
- Rank and score leads according to the SVM classifier model.  Age and Single Marital status will have the most positive impact. 
- After 2.5 contacts, people stop converting.
- The longer the call duration, the better chance that there will be a conversion, especially with a younger demographic.
- Work with the business to understand why they have so many contacts in the summer months.  With the cap of 2.5 they might concentrate more on the duration of call with younger prospects. 
