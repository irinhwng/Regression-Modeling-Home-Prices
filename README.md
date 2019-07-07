Presentation Slide: https://docs.google.com/presentation/d/1phzle5SBAUBeMlTHaLtnNUP8Ee0QPOp_Yd4rWt2KU1Y/edit#slide=id.p

---

# Predicting Home Prices using Ames Housing Data 
---

## **Problem Statement**

The real estate industry, like the rest of world, is poised to adopt new technologies. For example, Amazon- the pioneer of E-commerce- created a ripple effect that drastically changed the retail sector. On the other hand, companies like Uber are altering the need for residential garage space. Data- nowadays-  is a commodity (especially for millenials). This poses a problem for the real estate industry- particularly in the housing market. In addition to millenials' reliance on data, millenials are experiencing a housing crisis; it is very difficult for young families to purchase homes. Therefore, it is integral for Zillow to create a regression model that will predict the sale price of a home accurately. 

This project will use the Ames housing data. This data set contains information from the Ames Assessor’s Office used in computing assessed values for individual residential properties sold in Ames, IA from 2006 to 2010. To test the validity of our model, we will focus on four main metrics (Training R-Squared, Test R- Squared, Training RMSE, and Test RMSE). A successful R-squared will be very close to 1 while a successful RMSE will be close to 0. 

Remember, this project is for Zillow (an online neighborhood real estate site). This project is important for two reasons: 
- Smartphones are leading consumers to first use their phones to peruse houses before contacting a real estate firm (especially young families and millenials)
- Millenials are having a problem with affordable housing; thus, it's integral for us to predict the sale price of homes accurately in order for our users to understand the true price and target their goal. 
--- 

## **Data Cleaning and EDA**

**Data Summary:** http://jse.amstat.org/v19n3/decock/DataDocumentation.txt

#### Assessing Missing Values
- All missing values were imputed properly. By looking at the Ames data summary, object columns that have empty values indicate the feature of that house is non-existant. For example, if a particular cell under `basement cond` is empty, it means that specifc house does not have a basement. This is the same for numeric columns. To refrain from deleting rows from our training data, I filled all empty "numeric" cells with 0 and all empty "object" cells with string "none". 
- In this dataset, there were 4 columns that were missing a lot of data (three columns were missing ~95% and one column was missing ~50%). Due to high amount of missing cells for those 4 columns, I removed them from our data set. 

#### Distributions of Target Variable `SalePrice`
- Our target variable `SalePrice` has a right-skewed distribution 
- For this project, we will not execute a log transformation of `SalePrice`

#### Key Data Cleaning and EDA Notebook
- Please look at `CLEAN.ipynb`
- This notebook shows my step by step process of cleaning the train data. 
---

## **Preprocessing and Modeling**

#### Assessing Validity of Categorial Columns
- After cleaning my data, I created a big dataframe that created dummy columns from the categorical variables. Ultimately, I did this to find the dummy columns with the highest correlation to `SalePrice`. 
- My three dummy columns I picked for my group of features are: `Foundation_PConc`, `Bsmt Qual_Ex`, `Kitchen Qual_Ex`
- Please open the `Dummy` notebook to see how I executed important categorical columns. 

#### Manufacturing Columns
- In the `CLEAN.ipynb` notebook, I manufactured three columns: `homeage`, `baths`, `garageage`
- Here is a data dictionary for my engineered columns:

|Column Name|Equation|
|---|---|
|home age|Yr Sold - Yr Built|
|baths|Full Bath + (Half Bath)/2|
|garage age|Yr Sold - Garage Yr Built|

#### Scaling and Polynomial Transformation of the Data 
- In the `PreProcessing.ipynb` notebook, I scaled the data using the mean and standard deviation of the data from train.csv 
- In the `TEST_SETUP` notebook, I used the training data's mean and standard deviation to scale our test data. 
- In the `PreProcessing.ipynb` notebook, I executed a polynomial transformation of the data excludng our three dummy columns. 

#### Train Test Split 
- In the `MODELING.ipynb` notebook, I executed the train test split method to implement a non biased test of our model. 

#### Variety of Models Used
- We used four models to determine best fit (LinearRegression, Lasso, Ridge, and Elastic). Please look at the `MODELING.ipynb` notebook for further implementation. 
- To verify our best fit model, we executed a GridSearch method to determine the best parameter for the Elastic model since Elastic involves both Ridge and Lasso. After finding our R-Squared and RMSE metrics, we compared those metrics with the model of choice from `MODELING.ipynb`. 
- To see how we executed our GridSearch method, please open `AMES_Gridsearch1.ipynb` for further implementation. 

#### Baseline Model + Visualizations 
- To see the effect of our model, we must look at the scores of our baseline model. 
- Please open `Visualization_Baseline.ipynb` to see the execution of our baseline metrics and distributions and scatterplots of our important features
---

## **Evaluation and Conceptual Understanding**

- Since we are executing polynomial transformation and scaling our data, it is hard to pick certain features that'll effect the sale price of homes. 
- But through our modeling steps, we can bring insight on how to create an effective model that can predict accrurately. 

#### Results

|Metric|Result|
|---|---|
|Train Score|.9283|
|Test Score|.9037|
|Train RMSE|21,427|
|Test RMSE|24,064|

---

## **Conclusion**

- Our main conlusion for this project is that we created a regression model that can accurately predict the Sale Price of homes. According to the RMSE, we're off by our predictions on average by approximately $24,000.00. This can be detrimental for certain neighborhoods. For example, the median price for a 2 bedroom apartment in Manhattan is $1.5 Million. Using our model method in Manhattan may satisfy Zillow customers more than people living in Ohio where the average sale price of a home is $155,000.00. 
- If this regression model were to be initiated, Zillow should implement this price calculator only for homes in Los Angeles, New York, San Francisco, Palo Alto, Urban Honolulu. 
---

## **Recommendations**

- It would be very helpful to get the appropriate interest rate during the time of the homebuyer purchasing the house. Personally, my mom doesn't want to sell our house in the valley since the interest rates are high. Factors like this plays a big role in home buying. So having an additional column of interest rates would have been very helpful. 
---

## **Sources**

- http://jse.amstat.org/v19n3/decock/DataDocumentation.txt
- https://www.nar.realtor/commercial-connections/top-ten-issues-affecting-real-estate
- https://www.nytimes.com/2015/01/18/realestate/what-750000-buys-you-in-new-york-city.html
- https://www.usnews.com/news/best-states/slideshows/10-most-affordable-states?slide=11
- https://www.usatoday.com/story/money/2019/04/04/what-it-actually-costs-to-live-in-americas-most-expensive-cities/37748097/
- https://www.bloomberg.com/news/articles/2019-05-18/three-charts-show-struggle-is-real-for-millennial-home-buyers
- https://www.pewresearch.org/fact-tank/2018/05/02/millennials-stand-out-for-their-technology-use-but-older-generations-also-embrace-digital-life/
- https://www.zillow.com/ames-ia/home-values/
- https://medium.com/@samchaaa/preprocessing-why-you-should-generate-polynomial-features-first-before-standardizing-892b4326a91d
---

## **Worflow of Notebooks**

- This image visualizes my workflow for this project

<img src= "./Workflow.png">
