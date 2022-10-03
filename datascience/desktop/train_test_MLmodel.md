# Train and test a machine learning model 

Let's train a couple of machine learning models to classify the emails in the dataset as containing either spam or ham. In this section, we train a decision tree model and a random forest model. Then, we test the accuracy of the predictions. 

> **Note:** 
The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the DSVM. 

First, let's split the dataset into training sets and test sets: 

```R
rnd <- runif(dim(data)[1]) 
trainSet = subset(data, rnd <= 0.7) 
testSet = subset(data, rnd > 0.7) 
```

Then, create a decision tree to classify the emails: 

```R
require(rpart) 
model.rpart <- rpart(spam ~ ., method = "class", data = trainSet) 
plot(model.rpart) 
text(model.rpart) 
``` 

Here's the result: 

![decision tree example](https://raw.githubusercontent.com/ianl-terawe/academy/main/datascience/desktop/media/decision_tree_example.png "decision tree example")

To determine how well it performs on the training set, use the following code: 

```R
trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class") 
t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred) 
accuracy <- sum(diag(t))/sum(t) 
accuracy 
```

To determine how well it performs on the test set: 

```R
testSetPred <- predict(model.rpart, newdata = testSet, type = "class") 
t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred) 
accuracy <- sum(diag(t))/sum(t) 
accuracy 
```

Let's also try a random forest model. Random forests train a multitude of decision trees and output a class that's the mode of the classifications from all the individual decision trees. They provide a more powerful machine learning approach because they correct for the tendency of a decision tree model to overfit a training dataset. 

```R
require(randomForest) 
trainVars <- setdiff(colnames(data), 'spam') 
model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam) 
 
trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class") 
table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred) 
 
testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class") 
t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred) 
accuracy <- sum(diag(t))/sum(t) 
accuracy 
```

