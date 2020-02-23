library(readr)
library(ggplot2)
library(dplyr)

#data that we are going to analyze and submit
test <- read_csv("test.csv")
#data we used to manipulate and test out hypothesis
training <- read_csv("train.csv")
#this is how we want our submission to look like
sample_data <- read_csv("sample_submission.csv")


#combine the training and test data sets so that we can properly train our model.
#the training set has the sale price of each property but the test set d/n (since
#that is what we're trying to predict).

#first add SalePrice variable to test set.
#NOTE: this will create new data set with the new column as opposed to adding new
#column to data set that already exists
test2 <- as_tibble(data.frame(SalePrice = rep("None", nrow(test)), test[,]))
#before combining data sets you need to clean up both the test2 and training data sets
#       1. test2 has 3 columns not in training: X1stFlrSF, X2ndFlrSF, X3SsnPorch
#       2. in training those 3 parameters are known as: 1stFlrSF, 2ndFlrSF, 3SsnPorch

#rename columns in training or test2. here we are renaming columns in test2 to match those of training
names(test2)[names(test2) == "X1stFlrSF"] <- "1stFlrSF"
names(test2)[names(test2) == "X2ndFlrSF"] <- "2ndFlrSF"
names(test2)[names(test2) == "X3SsnPorch"] <- "3SsnPorch"

#now combine data
data_combined <- rbind(training, test2)
str(data_combined)

#change sale price for char to numeric
data_combined$SalePrice <- as.numeric(data_combined$SalePrice)

#median < mean so prices are skewed to the right
summary(data_combined$SalePrice)

#potential categories to look at and hypothesis
#       Primary 
#       -Neighbourhood, Condition1, Condition2: location, location, location
#       -BldgType: detached > 2 fam conversion > duplex > twnhouse end unit > twnhouse inside unit
#       Secondary
#       -HouseStyle: building w. more stories and buildings with completed stories will have higher
#                    value
#       -OverallQual, OverallCond: quality matters but will be superceded by location but high 
#                                 + good location can skew price likewise in the other direction
