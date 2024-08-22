# Practical Application Assignment 17.1: Comparing Classifiers

Assignment 17.1 is a python project showing my ability to apply the full CRISP=DM framework while comparing the performance of the classifiers (k-nearest neighbors, logistic regression, decision trees, and support vector machines) you encountered in this section of the program.  


## Contact 
If you want to contact me you can reach me at contactbethford@gmail.com

  
  
## Files
* 17.1.ipynb - Main python script with full charting and data
* 
* 
* README.md

## Objective


## Data
The dataset comes from the UCI Machine Learning repository Links to an external site. The data is from a Portuguese banking institution and is a collection of the results of multiple marketing campaigns. In an effort to use the data to determine who to best target for term deposits. While the job variable had 11 different values, I paired down to two variables based on income type: those with a steady income versus more variable types.  Additonally I mapped months, default, housing and loan to numericals.  I added a new field to account for not only how long a conversation was, but also how often they happened in order to account for the investment in total time. Variable potcome was dropped as we had too much missing data.  Additonally, I dropped the default variable as their were only 815 values, and people on default are too much of a business risk. 

## Methodology
I first looked to the correlations to the Y variable.  I then transformed the categorical variables and then scaled the numericals. I rechecked correlations with transformations in place. 
I then ran a Lasso regression to see if there were significant non zero variables.  Without success, I first tried to run the different types of classifiers.  The svc classifier would not run to completion on my computer.  I knew that I still needed to reduce the variables.  To that end, I moved on to a principal component analysis with 2 components.  Based on these results, I was able to create a reduced testing sets based on the top features. 



**Modeling:**
- 151,550 records
- Variables - Top Features, ['age','duration', 'totalTime', 'marital_single', 'marital_married', 'y']
- I ran five different classifier models (LogisticRegression(2), DecionTrees, KNearestNeighbor, SupportVectorMachines )
- I ran cross validation on the strongest model of SVM, which validated the accuaracy scoresa 
- With the recall and precision at 0, I realized that I needed to weight the classes to make them more balanced.  With this method, the recall and precision rose.
- I then tested out different types of kernels with sigmoid and rbf, but linear stayed with the highest accuracy.  


**Overall Findings**
- Ridge model was the best performing model, indicating that the larger price values may need to be handled differently
- The R2 was only .3186 indiacting that this model may only be identifying approximately one-third of the drivers for this model.

![Picture of a bar chart showing linear SVM is the best choice.](/images/ModelPerformance.png)


**Coefficients**
- Insights that came out of this include that the duration of a call was more important on seccess of a term deposit than the toal time with frequency. Amount of time that have gone between. 

- Harley Davidson drove the lowest price but this is most likely due to the harley being a motorcycle so inherently less expensive than a car
- Fuel type was also not a driver of price with coefficients less than -0.5

## Recommendations
- Keep more Trucks and Convertibles in stock as this will increase your the dealer's prices.  See image "Ridge Coefficients Greater than .25".png
-  Rear Wheel Drive (RWD) is a stronger driver than Front Wheel Drive (FWD) See image "Ridge Coefficients Less Than -.1".png
- Car manufacturer is key.
- The created field 'age' might have had multicolinearity with the odometer log, but age had a much higher negative impact than odometer. 
- Ask the client specifics on types of manufacturers they will have on their lot.  This may get rid of some luxury vehicles examined for better results.
- Data quality was an issue here with alot of nulls.  Try running some models on smaller data sets that have more fields to consider in the regression models.
