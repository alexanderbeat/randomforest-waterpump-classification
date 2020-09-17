# Flatiron Mod 3 Project - Tanzania Water Pump Classification with RandomForest


# Prerequisites
Runs on latest version of Python. Uses Sci-kit Learn RandomForest Classifier.  

# Overview

* Problem: Predict which Tanzanian water pumps are functional, which need repairs, and which don't work at all. Predict one of these three classes based on a number of variables about what kind of pump is operating, when it was installed, and how it is managed. A smart understanding of which waterpoints will fail can improve maintenance operations and ensure that clean, potable water is available to communities across Tanzania. 
* Audience: Main audience is the pump management companies who handles repairs and construction, along with city officials who work with companies to make decisions on pump location and technology for the pumps used. 
* Business Questions: Do older pumps need more repairs or are more prone to breaking? What is the relationship between population and working or nonworking pumps? Which type of pump to avoid?
* Business Value: A smart understanding of which waterpoints will fail can improve maintenance operations and ensure that clean, potable water is available to communities across Tanzania. This understanding includes predictability based on location and types of pumps, for faster assessment and follow through. 


# Content
The dataset contains 59,400 training samples and 14,850 test samples, with 40 different features. The training/test set values and training labels are stored in csv. Test set values were used for final testing and then stored as predictiondf_2.csv and submitted to [Drivendata](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/page/23/) competition site for accuracy. This site is where the dataset was obtained as well. 


## Feature Descriptions

* id number ** - don't need, will match with index
* amount_tsh - Total static head (amount water available to waterpoint)
* date_recorded - The date the row was entered **
* funder - Who funded the well **
* gps_height - Altitude of the well
* installer - Organization that installed the well **
* longitude - GPS coordinate
* latitude - GPS coordinate 
* wpt_name - Name of the waterpoint if there is one **
* num_private - **
* basin - Geographic water basin **
* subvillage - Geographic location **
* region - Geographic location **
* region_code - Geographic location (coded) ++
* district_code - Geographic location (coded) ++
* lga - Geographic location **
* ward - Geographic location **
* population - Population around the well
* public_meeting - True/False **
* recorded_by - Group entering this row of data **
* scheme_management - Who operates the waterpoint ++ **
* scheme_name - Who operates the waterpoint ++ **
* permit - If the waterpoint is permitted **
* construction_year - Year the waterpoint was constructed
* extraction_type - The kind of extraction the waterpoint uses ++ **
* extraction_type_group - The kind of extraction the waterpoint uses ++ **
* extraction_type_class - The kind of extraction the waterpoint uses ++
* management - How the waterpoint is managed ++ **
* management_group - How the waterpoint is managed ++
* payment - What the water costs **
* payment_type - What the water costs ++
* water_quality - The quality of the water **
* quality_group - The quality of the water ++
* quantity - The quantity of water **
* quantity_group - The quantity of water ++
* source - The source of the water **
* source_type - The source of the water ++
* source_class - The source of the water ++ **
* waterpoint_type - The kind of waterpoint **
* waterpoint_type_group - The kind of waterpoint

# Method
Tested three different algorithm models:
* Ran several models to find best performance of classification. 
* Looked at most important features involved in classification from model evaluation.
* Followed up with visuals to help explain each variables effect on class.
* Focused mainly on location, population and gravity well pump technology.

### Best Model Performance
A RandomForest classifier model proved to have the highest performance with little overfitting and a classification accuracy of 79%. A grid search was used to find the best parameters for this model. 

train acc: 0.9999857720106995
test acc: 0.7880113912620685


Classification Report:

![classreport](https://github.com/alexanderbeat/randomforest-classification-project/blob/master/images/rf_classreport.png)


Confusion Matrix and most important features for classification:

![matrix](https://github.com/alexanderbeat/randomforest-classification-project/blob/master/images/output_162_1.png)

# Partial Dependence Plots for feature importance. 
Chosen features:

* Longitude & Latitude
* Population
* Extraction type: Gravity pump

### Longitude and Latitude
Nonfunctional pumps likely to be located:
* Latitudes between -9 to -1. 
* Below 34 degree longitude and above 37 degrees longitude

![pdp](https://github.com/alexanderbeat/randomforest-classification-project/blob/master/images/output_171_0.png)
![pdp](https://github.com/alexanderbeat/randomforest-classification-project/blob/master/images/output_171_1.png)


### Population
* Nonfunctional pumps likely to be located near smaller population concentration or zero population.
* Focus on those pumps first for replacement if not dry. 
* Repairs: Pumps near 0 population and pumps near high population with high use.

![pdp](https://github.com/alexanderbeat/randomforest-classification-project/blob/master/images/output_171_5.png)


### Extraction type: Gravity pump
* High chance of needing repair
* Most likely functional. 
* Check on those as priority.
* Build different type, more resilient pumps. 

![pdp](https://github.com/alexanderbeat/randomforest-classification-project/blob/master/images/output_171_7.png)



# CONCLUSIONS & RECOMMENDATIONS

Location (Latitude and Longitude): 
> Wells are classified as functioning between 34-37 degrees longitude. You'll see that backed up by viewing the classification of nonfunctional for longitude as being near opposite in results, showing most telling below 34 deg longitude and above 37 degrees. Latitude classifies functioning best at -9.5 and -3 degrees. Repairs are needed mainly at pumps along latitude -11.5 degrees. Nonfunctioning pumps will be along latitudes from -9 to -1. Nonfunctional pumps will be located mostly between 250 and 1250 sea level. Perhaps a well has to work harder and requires more materials if the pump is higher above sea level which means more things that could break. 

Population:
> It seems that the lower population and remote wells are more likely to be nonfunctional. Could be because of less people around to notify authorities of the problem and is not needed. Pumps near high population on the other hand, have a higher chance of needing repair. So it'd be best to focus on repairs to wells near populations who need it most and then get to non-populated pumps second.

Gravity extraction pumps:
> Gravity extraction type pumps have a high chance of needing repair, but are often still functional, so check on those pumps as priority and also focus on not building more of that type, focusing on more resilient type of pumps. 

For future feature selection and engineering: 
- Look at skewed 0s in long, lat that I removed, population, cnstruction year and amount tsh. 
- Construction year is very skewed but still important because the older wells could be falling apart. You'll see that the older a pump is the higher chance of it being nonfunctional or in need of repair. 
- If the well is dry, then the pump is most likely broken or in need of repair, although fixing it should be lower priority since it is not in use.  
- Lower total static head amount shows a higher chance of being broken. Pumps at 0 tsh are most likely broken. 
- Quantity labeled as enough most likely functioning. 



# Github Contents and Materials
* The notebook [student.ipynb](https://github.com/alexanderbeat/randomforest-classification-project/blob/master/student.ipynb) includes all code for models and evaluation. 
