# Will the customer subscribe to a term deposit?
## An analysis of a bank's marketing campaign dataset

 ### Overview

In this investigation, we explore a dataset from a Portuguese banking institution, which is a collection of the results of multiple marketing campaigns. Our goal is to understand what type of classifier is best able to predict whether a customer will subscribe to a term deposit account. We consider the following classifiers:  <b>k-nearest neighbors, logistic regression, decision trees, and support vector machines </b>. As a result of the analysis, we provide to our customer -- the bank -- an optimal classifier to use to predict whether a prospective depositer will subscribe to the product (a term deposit).

### Data Understanding

We visualize the data in tablular form to get familiar it, as follows: 

* View the data and understand the meaning of the various features (columns) of the data
* Identify incomplete data and decide upon a reasonable apporoach to handling such data.
* Get a feel for how closely correlated the features are to each other. This will help us understand if there are redundant features which do not add significantly to data understanding. 

### Data Preparation And Cleanup
We drop columns that are not useful characterestics for modeling - <b>'month'</b> and <b>'day_of_week'</b> of last contact. In particular, we drop <b>'duration'</b> (duration of last contact) since that is the final contact where the customer accepts or rejects opening an account - it is essentially the same as the final outcome. We also drop drop <b>'pdays'</b> - the number of days since last contact - since most customers were not contacted (sparse data). In hindsight, we drop the only row with education = 'illiterate' since it gives a runtime error.

### Correlations in the data
Below is a heatmap that shows correlations between numeric features.
![CorrHeatmap](https://github.com/Vamana/Bank-Marketing-Analysis/assets/7783577/1bd9e2d7-c906-4e63-af30-6f5c8a40b617)

We observe that some numeric variable pairs like <b>(nr.employed, euribor3m)</b> and <b>(emp.var.rate, euribor3m)</b> have a <b>very strong positive correlation</b>. This is rather surprising and indicates a <b>possible bias in the data</b>, since the  Euro Interbank Offered Rate (euribor) should a-priori have no connection with number of employees (nr.employed) or employment variation rate (emp.var.rate)

### Preprocessing the data
We use an <b> OrdinalEncoder </b> to encode categorical data. This is reasonable in this context because we are interested in a class prediction (yes/no), given a new data point. For this classification purpose, there is no implied hierarchy or importance attached to any specific numeric value that we convert a categoric value to. We just need to map each categorical feature to <b><i>some</i></b> numeric value so that the numeric algorithms can process the data.

### Classifier Models and Evaluation
We built a model for each classifier, trained each model with the database and evaluated the models by calculating an accuracy score. We also profiled the computational performance of each model.

#### Model Accuracy
Below is a bar plot of accuracy (maximum score = 1) for each model.
![ModelAccuracy](https://github.com/Vamana/Bank-Marketing-Analysis/assets/7783577/91d20e18-d7c0-4065-b025-40a64763e30e)
While all models had a reasonably high accuracy (> 85%), <b>Logictic Regression</b> and <b>Support Vector Machines</b> stood out with a <b>90%</b> accuracy. <br/>

#### Model Computational Performance
Below is a bar plot of computational performance (measured in seconds) for each model.
![ModelPerformance](https://github.com/Vamana/Bank-Marketing-Analysis/assets/7783577/f572c3ec-ec1e-422a-9d2c-6115842bcf7f)
The <b> K Nearest Neighbors Classifier </b> stood out as easily being the fastest computationally, while <b> Support Vector Machines</b> was the poorest performer by a significant margin. <b>Logistic Regression </b> had moderate performance characterestics.

### Recommendations
Based on the results of our Machine Learning models, considering both Model Accuracy with Computational Performance, we can recommend that <b>Logistic Regression</b> is the best model to use to predict customer subscription to the bank's term deposit product.

### Next Steps
It will be useful to dive deeper into the very strong correlation between the feature pairs <b>(nr.employed, euribor3m)</b> and <b>(emp.var.rate, euribor3m)</b>. As noted earlier this could indicate a <b>possible bias in the data</b>, since the  Euro Interbank Offered Rate (euribor) should a-priori have no connection with number of employees (nr.employed) or employment variation rate (emp.var.rate)







