# Modeling Property Sales in Ames, IA

## Project Map
 - [Presentation Deck](./slides.pdf)
 - [Code](./code)
  - [Cleaning and Preprocessing](./code/01_Cleaning_Preprocessing.ipynb)
  - [EDA and Feature Engineering](./code/02_EDA_and_Feature_Engineering.ipynb)
  - [Modeling](./code/03_Modeling.ipynb)
  - [Kaggle Submission](./code/04_Kaggle.ipynb)
 - [Images](./images)
  - [Multicollinearity Example](./images/AboveGradeLivingAreaAnd1stFlrSFByZoning.png)
  - [Sale Price vs Property Area](./images/AboveGradeLivingAreaAndSalePriceByZoning.png)
  - [Area Features Correlated with Sale Price](./images/AreaFeaturesCorrelationwithSalePrice.png)
  - [Distribution of Area Features](./images/AreaHistograms.png)
  - [Sale Price by Garage Area](./images/GarageAreaAndSalePriceByZoning.png)
  - [Sale Price by Lot Area](./images/LotAreaAndSalePriceByZoning.png)
  - [Sale Price by Zoning](./images/SalePricesByZoning.png)
 - [Data](./data)
  - [Training Data](./data/train.csv)
  - [Testing Data](./data/test.csv)
  - [Submission](./data/submission.csv)

### Contents:
- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Data Dictionary](#Data-Dictionary)
- [Conclusions](#Conclusions)

### Problem Statement 

Generalizing a property price predictor to many cities is a difficult task.  Different data is collected in different regions.  Neighborhoods and ZIP codes lose meaning.  Climate and geography varies property features, building materials, and building standards.  However, some property qualities have ubiquitous value.  One such is square footage and another is zoning.  Intuitively increased square footage should increase property value. Zoning serves as proxy for neighborhood and quality of features that is translatable across all features.  The central investigation of this project is to determine if a multiple linear regression can accurately predict housing prices in Ames based on square footage values and zoning values. Additionally, this project seeks to answer the relative impacts of square footage metrics and zoning on property prices. 

### Executive Summary

This notebook is divided into five notebooks. The majority of the code is in the "helper function" notebook.  The remaining four notebooks walk through the data science process making heavy use of the helper functions.  Most of the modeling process including cleaning, preprocessing, model selection, modeling, and model evaluation are compressed into one helper function: model.  This makes it easy to quickly swap out features and see the impact on model performance. 

### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**Lot Area**|*int64*|model_ready|Lot size in square feet| 
|**Gr Liv Area**|*int64*|model_ready|Above grade (ground) living area square feet| 
|**Garage Area**|*float64*|model_ready|Size of garage in square feet| 
|**MS Zoning_FV**|*uint8*|model_ready|Dummy column indicating if property is zoned for floating island residential| 
|**MS Zoning_I (all)**|*uint8*|model_ready|Dummy column indicating if property is zoned for industrial| 
|**MS Zoning_RH**|*uint8*|model_ready|Dummy column indicating if property is zoned for residential high density|
|**MS Zoning_RL**|*uint8*|model_ready|Dummy column indicating if property is zoned for residential low density|
|**MS Zoning_RM**|*uint8*|model_ready|Dummy column indicating if property is zoned for residential medium density|

### Conclusions

This project had two goals. The first goal was to determine if property characteristics and zoning ordinance can predict sale price. The second goal was to determine what the impact of property area and zoning are on sale price. These features were selected for their ability to generalize to many US cities. An accurate model soley based off of square footage and zoning would be a powerful and simple predictor of price applicable across the US.

With respect to the first goal, our ultimate model, a multiple linear regression combining living area, garage area, lot area, and zoning ordinance, proved to be an unreliable predictor of sale prices in Ames, Iowa.  Due to its simplicity, the model was not overfit.  However, its R2 score of 0.63 paled in comparison to the baseline models 0.85 R2 score.  Square feet and zoning ordinance do not contextualize each other enough to predict price.  Additional information is needed to create a reliable model.

With respect to the second goal, a linear regression is a white-box model and so can be inferred upon to determine the relative effect of features on price.  Analysis of the linear regression coefficents determined the following:

Increase in lot area by one square meter results in an increase in price by 0.50 dollars.  

Increase in garage area by one square meter results in an increase in price by 75 dollars.

Increase in living area by one square meter results in an increase in price by 130 dollars.

Ranking impact impact of zone on price:
Floating Village
Low Density
Medium Density
High Density
Commercial
Industrial
Agricultural


Aside from the results of the modeling, it is import to consider the following context:
- Zoning is not as generalizable as we want it to be. Two cities can have vastly different zoning practices and the process has become more political than practical. We can no longer rely on an economic center to be zoned for high density because of factors like gentrification and NIMBYism.
- In an ideal setting, where zoning ordinances are more specific, more responsive to the spatial economy, and more consistent across cities and states, zoning could be a really reliable predictor of price.
