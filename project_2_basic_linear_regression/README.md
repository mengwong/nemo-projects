# Predicting Housing Prices with Ames Housing Data, by Yap Jun Hong (Nemo)

## Summary of the project

Predicting housing prices and knowing what features affects housing prices the most is valuable for both companies and homebuyers. This project aims to use Linear Regression and its variants, Lasso, Ridge, and ElasticNet, to infer the features that most affect housing prices. A secondy goal is to predict housing prices on a test set and compare the results against others on Kaggle.

There are several features that are positively correlated with the response variable, the sale price of a house. The strongest correlation is the overall quality of the house with a strength of 0.8. The ground living area is also important, with a strength of 0.72. The conclusion is that a bigger house that is of better quality and in a better condition fetches the best prices. 

This project is a good stepping stone to a larger project that compares housing features in different towns. 


## Section 1: Problem Statement

This project is for primarily for companies that build, purchase, and sell houses. The secondary audience is for the homebuyer who wishes to buy a new house or know what to focus on for renovation

### 1.1: Why Predicting Housing Prices Matter

Between 2006 and 2010, The [Ames Assessor's Office](https://www.cityofames.org/government/departments-divisions-a-h/city-assessor) collected data on houses in the city of Ames, located in Central Iowa. While the intended purpose for this dataset was for tax purposes, the dataset can also be used to predict housing prices. 

Being able to predict housing prices allows companies and consumers a quick way to gauge whether the prices being offered are fair for both parties. Even if the house sells for higher or lower
 than the predicted price, having a fair price that both parties can refer to can reduce psychological effects of pricing and make the bargaining process more fair. I am referring to how some companies use [comparative pricing](https://www.entrepreneur.com/article/279464) to make a price seem higher or lower. This trick works by offering a high, unfair price initially, and then lowering the price to make the lowered price seem more attractive, even if the lowered price is still higher than what's fair.

### 1.2: Business Context

In this project, I am acting as a consultant who has been asked to look through this dataset and predict housing prices for a company specialising in selling property. As they are familiar with the basics of data science, they have asked for something not too complex that they can understand. **I will run a Linear Regression model and its variants, Ridge, Lasso, and ElasticNet**, to predict the prices.

### 1.3: Inference, Knowing What Gives the Advantage

While this is a secondary goal in this notebook, linear regression has the advantage of being very well studied and explored. This means that the model is easily interpretable, which means we can figure out which features affect housing prices.

Knowing what features affect housing prices is useful for companies and consumers. For businesses, if the number of bedrooms increases house prices by a factor of 5 and the number of bathrooms increases house prices by a factor of 2, then companies can optimise for the number of bedrooms and bathrooms to build given their limited resources. Combine this knowledge with knowing which locations command the highest markup price, and companies can begin to guess which areas would be more competitive to bid for.

On the consumer side, knowing what factors are important for housing prices will help buyers learn what they should look out for. This means that buyers can ask salespersons why a house is priced the way it is and know whether the house is abnormally priced.

### 1.4: Kaggle Competition

To check how my predictions compare with other data scientists, I am also submitting my linear regression model to a kaggle competition. **Models are scored based on Root Mean Squared Error**.

### 1.5: The Dataset

The dataset used here is the Ames Housing Dataset. To my knowledge, it was released in 2018. As mentioned above, it is housing data from 2006 and 2010.

This dataset has [81 columns](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt) and is split into a training and test set. Both sets have 80 columns in common, with the test set having the target variable, 'Sales Price', removed. 

While the dataset has too many features to list here, a list of important features is summarised below.

### 1.6: Measuring Success

Success will be measured by comparing my model's predictions with the provided test set. The difference between the two will be measured using Root Mean Squared Error (RMSE) in Kaggle. In part, this is for convenience as it's the metric used in the Kaggle competition, but it's also useful as it's more sensitive to outliers than, say, Mean Absolute Error. As this data question involves housing and prices, there is bound to be right-skewed data, with some houses being priced much higher than others.

## Section 2: Notebooks in this project

1. [Data Cleaning](notebooks/01_data_cleaning.ipynb)
2. [Exploratory Data Analysis](notebooks/02_eda.ipynb)
3. [Prediction and Conclusions](notebooks/03_prediction_and_conclusion.ipynb)

## Section 3: Data Dictionary

There are 81 columns in this dataset. The full data dictionary can be found [here](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt). This section will give a summary of the data dictionary.

|**Index**|**Feature**|**Data Type**|**Description**|
|---|---|---|---|
|**1**|Order|Discrete|Observation Number|
|2|PID|Nominal|Parcel Identification Number|
|3|MS SubClass|Nominal|Identifies the type of dwelling involved in the sale|
|4|MS Zoning|Nominal|Identifies the general zoning classification of the sale|
|5|Lot Frontage|Continuous|Linear feet of street connected to property|
|6|Lot Area|Continuous|Lot size in square feet|
|7|Street|Nominal|Type of road access to property|
|8|Alley|Nominal|Type of alley access to property|
|9|Lot Shape|Ordinal|General shape of property|
|10|Land Contour|Nominal|Flatness of the property|
|-|-|-|-|
|**11**|Utilities|Ordinal|Type of utilities available|
|12|Lot Config|Nominal|Lot Configuration|
|13|Land Slope|Ordinal|Slope of property|
|14|Neighborhood|Nominal|Physical locations within Ames city limits|
|15|Condition 1|Nominal|Proximity to various locations|
|16|Condition 2|Nominal|Proximity to various conditions|
|17|Bldg Type|Nominal|Type of dwelling|
|18|House Style|Nominal|Style of dwelling|
|19|Overall Qaul|Ordinal|Rates the overall material and finish of the house|
|20|Overall Cond|Ordinal|Rates the overall condition of the house|
|-|-|-|-|
|**21**|Year Built|Discrete|Orginal construction date|
|22|Year Remod/Add|Discrete|Remodel date|
|23|Roof Style|Nominal|Type of Roof|
|24|Roof Matl|Nominal|Roof Material|
|25|Exterior 1|Nominal|Exterior covering on house|
|26|Exterior 2|Nominal|Exterior covering on house|
|27|Mas Vnr Type|Nominal|Masonry veneer type|
|28|Mas Vnr Area|Continuous|Masonry veneer area in square feet|
|29|Exter Qual|Ordinal|Evaluates the quality of the material on the exterior|
|30|Exter Cond|Ordinal|Evaluates the present condition of the material on the exterior|
|-|-|-|-|
|**31**|Foundation|Nominal|Type of foundation|
|32|Bsmt Qual|Ordinal|Evaluates the height of the basement|
|33|Bsmt Cond|Ordinal|Evaluates the general condition of the basement|
|34|Bsmt Exposure|Ordinal|Refers to walkout or garden level walls|
|35|BsmtFin Type 1|Ordinal|Rating of basement finished area|
|36|BsmtFin SF 1|Continuous|Type 1 finished square feet|
|37|BsmtFinType 2|Ordinal|Rating of basement finished area|
|38|BsmtFin SF 2|Continuous|Type 2 finished square feet|
|39|Bsmt Unf SF|Continuous|Unfinished square feet of basement area|
|40|Total Bsmt SF|Continuous|Total square feet of basement area|
|-|-|-|-|
|**41**|Heating|Nominal|Type of heating|
|42|heatingQC|Ordinal|Heating quality and condition|
|43|Central Air|Nominal|Central air conditioning|
|44|Electrical|Ordinal|Electrical System|
|45|1st Flr SF|Continuous|First Floor square feet|
|46|2nd Flr SF|Continuous|Second Floor square feet|
|47|Low Qual Fin SF|Continuous|Low quality finished square feet|
|48|Gr Liv Area|Continuous|Above ground living area square feet|
|49|Bsmt Full Bath|Discrete|Basement full bathrooms|
|50|Bsmt Half Bath|Discrete|Basement half bathrooms|
|-|-|-|-|
|**51**|Full Bath|Discrete|Full bathrooms above grade|
|52|Half Bath|Discrete|Half bathrooms above grade|
|53|Bedroom|Discrete|Bedrooms above grade|
|54|Kitchen|Discrete|Kitchens above grade|
|55|KitchenQual|Ordinal|Kitchen quality|
|56|TotRmsAbvGrd|Discrete|Total rooms above ground|
|57|Functional|Ordinal|Home functionality|
|58|Fireplaces|Discrete|Number of fireplaces|
|59|FireplaceQu|Ordinal|Fireplace quality|
|60|Garage Type|Nominal|Garage location|
|-|-|-|-|
|**61**|Garage Yr Blt|Discrete|Year garage was built|
|62|Garage Finish|Ordinal|Interior finish of the garage|
|63|Garage Cars|Discrete|Size of garage in car capacity|
|64|Garage Area|Continuous|Size of garage in square feet|
|65|Garage Qual|Ordinal|Garage quality|
|66|Garage Cond|ordinal|Garage condition|
|67|Paved Drive|Ordinal|Paved driveway|
|68|Wood Deck SF|Continuous|Wood deck area in square feet|
|69|Open Porch SF|Continuous|Open porch area in square feet|
|-|-|-|-|
|**70**|Enclosed Porch|Continuous|Enclosed porch area in square feet|
|71|3-Ssn Porch|Continuous|Three season porch area in square feet|
|72|Screen Porch|Continuous|Screen porch area in square feet|
|73|Pool Area|Continuous|Pool area in square feet|
|74|Pool QC|Ordinal|Pool quality|
|75|Fence|Ordinal|Fence quality|
|76|Misc Feature|Nominal|Miscellaneous feature not covered in other categories|
|77|Misc Val|Continuous|Dollar value of miscellaneous feature|
|78|Mo Sold|Discrete|Month Sold|
|79|Yr Sold|Discrete|Year Sold|
|80|Sale Type|Nominal|Type of sale|
|-|-|-|-|
|**81**|Sale Condition|Nominal|Condition of sale|
|82|SalePrice (Target Variable)|Continuous|Sale price|

## Section 4: Recommendations

### Conclusion

In the end, the bigger the house, with a better rating of quality and condition, fetches you the highest prices. Even if you have the negative factors attached to the home, they only reduce prices by a factor of 1/5 or so (i.e. prices reduce by -6000 for every 30,000 increase in price, given ms_subclass and gr_liv_area). 

#### For Companies

For a given house, make sure that the quality and condition matches the one stated on paper. While it may be possible, though not advisable, to sell a BrkfacFace veneer at a more expensive price than expected, it's impossible to hide a house's quality and condition. If your company builds and sells property, you may want to build 1 story houses instead of 2 family conversions as it gives a better return of investment. However, watch out for market saturation: too many of the same type of house and the houses won't command as much money.

#### For Consumers

Location, location, location matters. Assuming you are someone most concerned with price, try to go for a cheaper neighborhood. But if you wish to stay at, say, NridgeHt, it's not the end of the world. Buy a more run down home and upgrade it yourself! Look for bedrooms above ground, and try to get a house that has a garage attached to it. Get an older house, not one built recently; the older the house the better. Make sure you don't buy a house with a basement. Get a house with a Brick Face veneer and renovate the house.

### Further Steps

With a linear regression model built for this town, perhaps building another linear regression model on a similar dataset for another town would be useful. With the two linear models, we can compare the coefficients and find out whether the same features play the biggest part in housing prices.

## Section 5: References

### References

(2020, July 17). _City Assessor_. City of Ames. [https://www.cityofames.org/government/departments-divisions-a-h/city-assessor](https://www.cityofames.org/government/departments-divisions-a-h/city-assessor)

Boachie, P. (2016, July 21). _5 Strategies of 'Psychological Pricing'_. The Entrepreneur. [https://www.entrepreneur.com/article/279464](https://www.entrepreneur.com/article/279464)

De Cock, D. _Ames Iowa: Alternative to the Boston Housing Data Set_. Truman State University. [http://jse.amstat.org/v19n3/decock/DataDocumentation.txt](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt)

Kuhn, M. & Johnson, K. (2019, June 21). _Feature Engineering and Selection: A Practical Approach for Predictive Models_. Taylor & Francis Group. [https://bookdown.org/max/FES/](https://bookdown.org/max/FES/)
