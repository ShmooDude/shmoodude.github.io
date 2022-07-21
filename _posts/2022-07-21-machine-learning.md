Machine Learning
================
Mark Gordon
2022-07-21

## K Nearest Neighbors

I found K nearest neighbors (kNN) the most interesting. The idea is to
use the closest k neighbors in order to predict the probability of the
response, with the highest probability being the chosen value. By
splitting the initial data into training and test data sets, we can then
get a misclassification rate to pick the optimal “k” value.

## Multi-class classification

``` r
# Load libraries
library(tidyverse)
library(caret)

# Read in iris data

# Split the data set
irisIndex <- createDataPartition(iris$Species, p = 0.8, list = FALSE)
irisTrain <- iris[irisIndex,]
irisTest <- iris[-irisIndex,]

# Training options
nfold <- 10 # number of cv folds
nrep <- 3 # number of times to repeat cv
pProcess = c("center", "scale") # preprocessing

# Train kNN model
knnFit <- train(Species ~ ., data = irisTrain,
                method = "knn",
                preProcess = pProcess,
                trControl = trainControl(method = "repeatedcv", 
                                         number = nfold, repeats = nrep),
                tuneGrid = data.frame(k = 1:20))

# Best Tune value
knnFit$bestTune
```

    ##   k
    ## 6 6

``` r
# Check model performance
confusionMatrix(data = irisTest$Species, 
                reference = predict(knnFit, newdata = irisTest))
```

    ## Confusion Matrix and Statistics
    ## 
    ##             Reference
    ## Prediction   setosa versicolor virginica
    ##   setosa         10          0         0
    ##   versicolor      0          9         1
    ##   virginica       0          0        10
    ## 
    ## Overall Statistics
    ##                                           
    ##                Accuracy : 0.9667          
    ##                  95% CI : (0.8278, 0.9992)
    ##     No Information Rate : 0.3667          
    ##     P-Value [Acc > NIR] : 4.476e-12       
    ##                                           
    ##                   Kappa : 0.95            
    ##                                           
    ##  Mcnemar's Test P-Value : NA              
    ## 
    ## Statistics by Class:
    ## 
    ##                      Class: setosa Class: versicolor Class: virginica
    ## Sensitivity                 1.0000            1.0000           0.9091
    ## Specificity                 1.0000            0.9524           1.0000
    ## Pos Pred Value              1.0000            0.9000           1.0000
    ## Neg Pred Value              1.0000            1.0000           0.9500
    ## Prevalence                  0.3333            0.3000           0.3667
    ## Detection Rate              0.3333            0.3000           0.3333
    ## Detection Prevalence        0.3333            0.3333           0.3333
    ## Balanced Accuracy           1.0000            0.9762           0.9545

<!-- rmarkdown::render("_Rmd/2022-07-21-machine-learning.Rmd", output_format = "github_document", output_dir = "_posts", output_options = list(html_preview = "false")) -->
