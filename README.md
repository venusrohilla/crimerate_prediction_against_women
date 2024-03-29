# Predicting rate of crime against women in the National Capital Territory of Delhi for the year 2015.

## Data Description
The dataset contains the data for crime rate against women in the NCT of Delhi aggregated by county.

## Data Attributes

1. county - county identifier
2. year - 2015
3. crmrte - crimes committed per person
4. prbarr - 'probability' of arrest
5. prbconv - 'probability' of conviction
6. prbpris - 'probability' of prison sentence
7. avgsen - avg. sentence, days
8. polpc - police per capita
9. density - people per sq. mile
10. taxpc - tax revenue per capita
11. west - =1 if in western Delhi
12. central - =1 if in central Delhi.
13. urban - =1 if in south Delhi.
14. pctmin- min minority 
14. wcon - weekly wage, construction
15. wtuc - wkly wge, trns, util, commun
17. wtrd - wkly wge, whlesle, retail trade
18. wfir - wkly wge, fin, ins, real est
19. wser - wkly wge, service industry
20. wmfg - wkly wge, manufacturing
21. wfed - wkly wge, fed employees
22. wsta - wkly wge, state employees
23. wloc - wkly wge, local gov emps
24. mix - offense mix: face-to-face/other
25. pctymle - percent young male

## Objective
1. To perform **univariate** and **bivariate exploratory analysis** of the dataset provided.
2. To develop a suitable **linear model with crmrte as the dependent variable** based on the EDA findings.
3. To explain the various aspects of the model used.

## Data Analysis & Data Cleaning

1. **The last column was getting read as 'object' data. It was found to be due to the special symbol at the last row, last column 0.074198931'**. Removed the special symbol from input csv file, to fix it.

2. It is to be noted that the **maximum value of probability features, prbarr & prbconv, are > 1** which is a data anomaly. prbpris & pctymle are found to be < 1.

3. There are 91 entries for all the 25 columns. Hence, there is **no missing value in the input dataset. Thus, no need to do data imputation** or to drop any feature.

4. The zeros for features, west, central and urban are expected, as the data is inherently boolean


**Observations**_<br/><br/>
_**From above analysis, it is found, that some rows have to be dropped before doing regression analysis. The probability values of some rows are found to be > 1 and location of one row was found to be both ’west’ and ’central’ at the same time. We will drop these rows before building the model. The special character error in the input dataset is also fixed.**_

## Univariate Analysis

Univariate visualization   provides summary statistics for each field in the raw data set. It is conducted **to find out how much a single feature in the dataset** would be helpful to determine the target feature, here in this case, crime rate.

<p align="center">
    <img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/uva.PNG">
</p>

![uvaf1](https://github.com/venusrohilla/crime-prediction-/blob/master/images/uvaf1.PNG)

![uvaf2](https://github.com/venusrohilla/crime-prediction-/blob/master/images/uvaf2.PNG)

![uvaf3](https://github.com/venusrohilla/crime-prediction-/blob/master/images/uvaf3.PNG)

_**Observation:<br/><br/>
The features density, mix, police per capita, probability of conviction and tax revenue per capita seems to have similar distribution as crime rate. But no definitive conclusion can be made from this observation. Lets examine further using bivariate analysis.**_

## Probability/ Cumulative Distribution Function (CDF)

![cdf1](https://github.com/venusrohilla/crime-prediction-/blob/master/images/cdf1.PNG)

![cdf2](https://github.com/venusrohilla/crime-prediction-/blob/master/images/cdf2.PNG)

_**Observations:**_<br/><br/>
_a) One **strange observation is in weekly wages of service industry (wser)**. More than 95% of wages lies below 400, but the maximum wage is around 2250. From the data, this is identified to be **county 185**. As the percentage of minorities in this county is high (nearly 65%) and wages in other sectors are comparatively less, the wages of service industry is mostly an error. We will remove **"county 185" from the input data**._ <br/><br/>
_b) Though the maximum value of tax revenue per capita is 120, more than 50% of values lies below 40._<br/><br/>
_c) Though the maximum value of police per capita is 0.009, more than 60% of values lies below 0.001._

## Bivariate Analysis

Bivariate visualization is performed to find the relationship between each variable in the dataset and the target variable of interest, i.e. crime rate. The plot of all features against crime rate is done as below.

![biv1](https://github.com/venusrohilla/crime-prediction-/blob/master/images/biv1.PNG)

![biv2](https://github.com/venusrohilla/crime-prediction-/blob/master/images/biv2.PNG)

_**Observations:**_ <br/><br/>
_a) Based on the above pairplot, it can be noted that **density is most positively correlated with crime rate. There is also some correlation with weekly wages under different domains but it needs further investigation, as they are not so pronounced.**_ <br/><br/>
_b) Strangely, the **weekly wage features and crime rate is found to be slightly positively correlated. This signifies unequal distribution of income** or probably high unemployment rate. One of the most important features that is not in the given data may be unemployment rate._ <br/><br/>

_**Lets try to find if there is any correlation among features for each location: ’west’, ’central’ & ’urban’.**_

## Correlation among features for each location: 'west', 'central' & 'urban'

Lets try to find if there is any correlation among features for each location: 'west', 'central' & 'urban'.

Number of data points in category: west is 23
Number of data points in category: central is 34
Number of data points in category: urban is 8

**Location: west**

![fcp1](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcp1.PNG)

![fcp2](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcp2.PNG)

![fcp3](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcp3.PNG)

![fcp4](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcp4.PNG)

![fcp5](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcp5.PNG)

**Location: central**

![fcpc1](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcpc1.PNG)

![fcpc2](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcpc2.PNG)

![fcpc3](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcpc3.PNG)

![fcpc4](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcpc4.PNG)

![fcpc5](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcpc5.PNG)

**Location: urban**

![fcpu1](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcpu1.PNG)

![fcpu2](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcpu2.PNG)

![fcpu3](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcpu3.PNG)

![fcpu4](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcpu4.PNG)

![fcpu5](https://github.com/venusrohilla/crime-prediction-/blob/master/images/fcpu5.PNG)

## Box Plots

Let's do the box plot & violin plot for the boolean features 'west', 'central', 'urban' to find impact on crime rate, if any.

![bp](https://github.com/venusrohilla/crime-prediction-/blob/master/images/bp.PNG)

## Violin Plots

![vp](https://github.com/venusrohilla/crime-prediction-/blob/master/images/vp.PNG)

**Observations:**_ <br/><br/>
_a) The crime rate in urban areas is found to be significantly high. Thus, the feature ’urban’ is an useful variable for prediction._<br/><br/>
_b) The crime rate in west is found to be less and central moderate. But as there is significant overlap, such variations may not be very helpful for prediction._<br/><br/>

## Feature-Feature Correlation Analysis

Many times, more than one input could be dependent on each other. In Linear Regression, the requirement is that all the input variables are independent of each other.

When a feature is dependent on one or more of the other input features, it leads to a phenomenon known as multi-collinearity. **Multi-collinearity among features can be identified by doing Feature-Feature correlation analysis**.

![hm1](https://github.com/venusrohilla/crime-prediction-/blob/master/images/hm1.png)

**Observations from the Feature HeatMap:**_ <br/><br/>
_a) The **density and urban variable seems to be highly correlated**, which is obvious, because urban areas are densely populated._<br/><br/>
_b) **Some of the "wage features" are positively correlated**, as the wage increase/ decrease in one domain would certainly influence the other. For example, **wtrd & wfir are positively correlated to wfed & wloc. Also, wfir and wtrd have moderate correlation.**_<br/><br/>

![hm2](https://github.com/venusrohilla/crime-prediction-/blob/master/images/hm2.png)

_**Observations from Zoomed Feature HeatMap:**_<br/><br/>
_a) Density and crime rate have a correlation of 0.73. But **density has high correlation with ’urban’ feature. Hence, whether both features, density and urban, are useful to predict crime rate needs further investigation. We wll use linear regression to sort out this question**._<br/><br/>
_b) The feature, ’urban’ has a correlation of 0.62 with crime rate, but whether the correlation is because ’urban’ has very high correlation with ’density’ is yet to be known._ <br/><br/>
_c) Wage columns, wfed & wtrd are positively correlated to ’density’ feature. This can be intuitively understood as the weekly wages would be higher in urban areas._<br/><br/>

## Conclusions

### Data Analysis and Cleaning

It is found, that **some rows have to be dropped** before doing regression analysis. The probability values of some rows are found to be > 1 and location of one row was found to be both ’west’ and ’central’, at the same time. We will drop these rows before building the model. The **special character error in the input dataset is also fixed**.

### Univariate Analysis

1. The features **density, mix, police per capita, probability of conviction and tax revenue per capita seems to have similar distribution as crime rate**. But no definitive conclusion can be made from this observation. 

2. One **strange observation is in weekly wages of service industry (wser).** More than 95% of wages lies below 400, but the maximum wage is around 2250. <br/> <br/> From the data, this is identified to be **county 185**. As the percentage of minorities in this county is high (nearly 65%) and wages in other sectors are comparatively less, the wages of service industry is mostly an error. We will remove **"county 185"** from the input data.

3. Though the maximum value of tax revenue per capita is 120, more than 50% of values lies below 40.

4. Though the maximum value of police per capita is 0.009, more than 60% of values lies below 0.001.

### Bivariate Analysis
1. Based on the above pairplot, it can be noted that **density is most positively correlated with crime rate. There is also some correlation with weekly wages under different domains but it needs further investigation, as they are not so pronounced.**

2. Strangely, the **weekly wage features and crime rate is found to be slightly positively correlated. This signifies unequal distribution of income** or probability of high unemployment rate. One of the most important features that is not in the given data is unemployment rate.

### Correlation among features for each boolean feature

1. Some of the correlation lines are showing upward or downward trends more than before.

2. **Probability of conviction is found to have negative correlation with crime rate in both west and central, but not in urban areas**.

3. **Tax Per capita is found to have positive correlation with crime rate in both central and urban areas**.

4. **Percentage of minority is positively correlated with crime rate, both in west and in urban areas**.

5. Thus, a combination of density and urban (or west or central) can help aid crime rate prediction.

6. However, there seems to be **not much data for 'urban areas'** to arrive at a conclusion.

### Linear Fit of Top Correlated Features

1. The crime rate in urban areas is found to be significantly high. Thus, the feature 'urban' is an useful variable for prediction.

2. The crime rate in west is found to be less and central moderate. But as there is significant overlap, such variations may not to be very helpful for prediction.

### Feature-Feature Correlation Analysis

1. Many times, more than one input could be dependent on each other. It leads to a phenomenon known as **multi-collinearity, which can be identified by doing Feature-Feature correlation analysis.** In Linear Regression, the requirement is that all the input variables are independent of each other.

2. The **density and urban variable seems to be highly correlated**, which is obvious, because urban areas are densely populated.

3. **Some of the "wage features" are positively correlated**, as the wage increase/ decrease in one domain would certainly influence the other. For example, **wtrd & wfir are positively correlated to wfed & wloc. Also, wfir and wtrd have moderate correlation**.

4. Density and crime rate have a correlation of 0.73. But **density has high correlation with 'urban' feature. Hence, whether both features, density and urban, are useful to predict crime rate needs further investigation. We wll use linear regression to sort out this question**.

5. The feature, 'urban' has a correlation of 0.62 with crime rate, but whether the correlation is because 'urban' has very high correlation with 'density' is yet to be known.

6. Wage columns, wfed & wtrd are positively correlated to 'density' feature. This can be intuitively understood as the weekly wages would be higher in urban areas.

### The above observations from EDA would be carried forward to help Linear Regression .

**==============================================================================**

# Linear Model on NCT of Delhi Crime Rate against women Dataset .

## Objective

To use insights from EDA to develop a suitable **linear model with crmrte as the dependent variable** and explain the various aspects of the model.

## Actionable Observations from EDA

1) The density and urban variable has highest correlation with crime rate.

2) But, density and urban variable seems to be highly correlated, which is obvious, because urban areas are densely populated. Hence, there is a high chance of multicollinearity between density and urban features. We wll use linear regression to sort out this question.

3) The feature, 'urban' has a correlation of 0.62 with crime rate, but whether the correlation is because 'urban' has very high correlation with 'density' is yet to be known.

4) A combination of density and urban (or west or central) can help aid crime rate prediction.

5) Wage columns, wfed & wtrd are positively correlated to 'density' feature. This can be intuitively understood as the weekly wages would be higher in urban areas.

6) Some of the "wage features" are positively correlated, as the wage increase/ decrease in one domain would certainly influence the other.

7) wtrd & wfir are positively correlated to wfed & wloc. Also, wfir and wtrd have moderate correlation with each other.

8) There are 6 strongly correlated values with Crime Rate: crmrte, density, urban, wfed, taxpc, wtrd.

## Evaluate Observations using Linear Regression Model

Lets evaluate the above observations by building Linear Regression Models, as it helps to understand the relation between variables better.

### Creating Model with Most Correlated Feature

**Interim Observations:**

a) As the p-value of density is 0 (small), the changes in crime rate has got close relation with changes in density.

b) R-squared value is found to be 0.525 with only density as predictor variable. This means that 52.5% variability of crime rate is explained by density feature.

c) Co-effient estimate of 0.0086 indicates one value increase of density would cause 0.0086 value increase in crime rate.

### Creating Model with Top 2 Correlated Features

**Interim Observations:**

a) **R-squared value is found to be slightly higher (0.527)** when the variable, 'urban' is coupled with density as predictor variables. But, R Squared always goes up when you add more variables regardless of whether the added variable help in prediction or not.

b) Adjusted R Squared, penalizes for adding more variables. Thus, it can go down when you add variables that don’t contribute. Here note that, **Adjusted R-squared value has gone down from 0.519 to 0.514. Also, the AIC value is increased from -470 to -469** (the smaller the AIC value, the better the model is).

c) It has been noticed that the **p-value of 'density' feature has been increased slightly**.

Thus, **the model has become more less reliable to explain crime rate**, because the feature 'urban' doesnt contribute to prediction. The confusion about the correlation between 'urban' and 'density' variable during EDA step, has been sorted out.

**Note:** If we add variables that are not meaningful as predictor, then it **would cause 'Overfitting'**. Then, prediction model would perform great with the training data but not with the real world data.

## Multiple Linear Regression: Model with all Features

<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/ml2.PNG">
</p>

<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/ml3.PNG">
</p>

<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/ml4.PNG">
</p>

## Removing features from all-feature Model

<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/rml2.PNG">
</p>

<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/rml3.PNG">
</p>

<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/rml4.PNG">
</p>

**Interim Observations:**

a) **Adj. R-squared improved** from 0.825 in all-feature model to 0.830, after removal of 2 features 'urban', 'county'.

b) **AIC value decreased** from -591.3 in all-feature model to -595.2, after removal of 2 features 'urban', 'county'.

Thus, **we have a better model than the all-feature model**. We will try to remove more features and analyze the model indicators.


<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/rml6.PNG">
</p>

<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/rml7.PNG">
</p>

**Interim Observations:**

a) **Adj. R-squared of the above model with 8 features dropped is better** than the all-feature model.

b) **AIC value of the above model is better** than the all-feature model.

Thus, **we have a better model than the all-feature model** by removing more features such as 'wmfg', 'prbpris', 'wloc', 'west', 'wtuc'. We will try to remove even more features with p > 0.05 and evaluate using RMSE.

## Model Evaluation Using Cross Validation & RMSE

We will test the change in RMSE value when the features with p > 0.05 are removed. The features with p > 0.05 are prbconv, mix, wfed, wtrd, wcon & avgsen. We will also check the RMSE values for the features removed in the previous model.

RMSE with None removed = 0.011598193103785095 <br/>
RMSE with wmfg removed = 0.01136661900197904 <br/>
RMSE with prbpris removed = 0.011775293806203662 <br/>
RMSE with wloc removed = 0.011190102338212366 <br/>
RMSE with west removed = 0.011516684556469887 <br/>
RMSE with wtuc removed = 0.010807252151383978 <br/>
RMSE with prbconv removed = 0.011772727414832405 <br/>
RMSE with mix removed = 0.012039673462990959 <br/>
RMSE with wfed removed = 0.011975451306453819 <br/>
RMSE with wtrd removed = 0.010915720261174582 <br/>
RMSE with wcon removed = 0.011764476830686559 <br/>
RMSE with avgsen removed = 0.011416545616172611 <br/>

<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/rmse.PNG">
</p>

<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/cv.PNG">
</p>

From the bar chart, the RMSE values performs better than 'None' when wtuc, wtrd, wloc, west, wmfg and avgsen are removed. Thus, in addition to the previous model, **wtrd & avgsen features are removed**. But the R-squared and AIC figures degrade when both the features are removed. Since wtrd has a higher p value, **we will remove wtrd in our model**.

The lowest cross validation MSE is for wloc, wtrd, prbconv and wcon. Thus, in addition to the previous exclusions, prbconv & wcon also can be dropped. But removal of either feature would increase the RMSE value as per the above plot. Thus, we will remove only wtrd in our model.

## OLS Regression Characteristic of Final Model


<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/fm2.PNG">
</p>

<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/fm3.PNG">
</p>

## Testing the Model on Input Data

<p align="center">    
	<img src="https://github.com/venusrohilla/crime-prediction-/blob/master/images/tm2.PNG">
</p>

## Conclusion

1. The Actual vs Predicted plot is linear. This signifies the prediction is working fine. The input data set is limited. With more data, the plot could be more linear.

2. As an improvement, we can combine the boolean features: west, central and urban into a single feature with categorical values 1, 2 & 3.. Such a feature can help aid the prediction.

3. If there is a chance to add features, then it might be helpful to get 'unemployment rate'.
