---
title       : DDP Project - Predicting Iris Species
subtitle    : Simple Shiny App to explore a Machine Learning Predictor
author      : C Palm
job         : Data Scientist
framework   : io2012 # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : github      #
widgets     : [bootstrap]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

#<style>
#.title-slide {
 #    background-image: url(http://cjpalm.github.io/DDP_project/images/screenShot.jpg);
#   }
#</style>



### Predicting Iris Species

* Machine Learning Algorithm to predict Iris Species
* Interactive - use to predict Iris Species based on Iris measurement
*    Or explore which factors are important to model prediction
*  Wrapped in a Shiny App for easy use

--- .class #id
### Data - Iris data from R datasets

```r
library(xtable)
options(xtable.type='html')
data(iris)
xtable(summary(iris))
```

<!-- html table generated in R 3.1.1 by xtable 1.7-4 package -->
<!-- Thu Dec 18 18:00:52 2014 -->
<table border=1>
<tr> <th>  </th> <th>  Sepal.Length </th> <th>  Sepal.Width </th> <th>  Petal.Length </th> <th>  Petal.Width </th> <th>       Species </th>  </tr>
  <tr> <td align="right"> 1 </td> <td> Min.   :4.30   </td> <td> Min.   :2.00   </td> <td> Min.   :1.00   </td> <td> Min.   :0.1   </td> <td> setosa    :50   </td> </tr>
  <tr> <td align="right"> 2 </td> <td> 1st Qu.:5.10   </td> <td> 1st Qu.:2.80   </td> <td> 1st Qu.:1.60   </td> <td> 1st Qu.:0.3   </td> <td> versicolor:50   </td> </tr>
  <tr> <td align="right"> 3 </td> <td> Median :5.80   </td> <td> Median :3.00   </td> <td> Median :4.35   </td> <td> Median :1.3   </td> <td> virginica :50   </td> </tr>
  <tr> <td align="right"> 4 </td> <td> Mean   :5.84   </td> <td> Mean   :3.06   </td> <td> Mean   :3.76   </td> <td> Mean   :1.2   </td> <td>  </td> </tr>
  <tr> <td align="right"> 5 </td> <td> 3rd Qu.:6.40   </td> <td> 3rd Qu.:3.30   </td> <td> 3rd Qu.:5.10   </td> <td> 3rd Qu.:1.8   </td> <td>  </td> </tr>
  <tr> <td align="right"> 6 </td> <td> Max.   :7.90   </td> <td> Max.   :4.40   </td> <td> Max.   :6.90   </td> <td> Max.   :2.5   </td> <td>  </td> </tr>
   </table>
Data Source:
Fisher, R. A. (1936) The use of multiple measurements in taxonomic problems. Annals of Eugenics, 7, Part II, 179â~@~S188.
Anderson, Edgar (1935). The irises of the Gaspe Peninsula, Bulletin of the American Iris Society, 59, 2â~@~S5.

--- .class #id

## How it works

* Used Random Forest algorithm - Split data into training test sets, evaluated model and use model to predict Iris type from input in Shiny App.
Here is the code used, Results of model applied to test data are shown:

```r
library(caret); data(iris); set.seed(1231); 
inTrain <- createDataPartition(y=iris$Species,p=0.60,list=FALSE); train <- iris[inTrain,]; 
test <- iris[-inTrain,]; modFit <- train(Species~.,data=train,method="rf",verbose=FALSE); 
varImport<-varImp(modFit); confusionMatrix(predict(modFit,test),test$Species)$table
```

```
##             Reference
## Prediction   setosa versicolor virginica
##   setosa         20          0         0
##   versicolor      0         18         1
##   virginica       0          2        19
```
* Only two of the factors are important, but left all four in the model, So users can explore the effect of each factor on the prediction.



--- .class #id

## Try It Out!

1. Predict Iris Species based on measurements you collect
2. Investigate which factors are important for prediction

https://cpalm-ds.shinyapps.io/DDP_project/
![Alt text](assets/img/screenShot.jpg)
