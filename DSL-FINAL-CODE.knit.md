---
title: "DSL FINAL CODE"
author: "Casper Collet and Chu Li"
date: "2025-03-29"
output:
  pdf_document: default
  html_document: default
---


``` r
#Written by: Casper Collet
library(readxl)

divorce_data <- read_excel("divorce.xlsx")
head(divorce_data)
```

```
## # A tibble: 6 x 55
##   Sorry_end Ignore_diff begin_correct Contact Special_time
##       <dbl>       <dbl>         <dbl>   <dbl>        <dbl>
## 1         2           2             4       1            0
## 2         4           4             4       4            4
## 3         2           2             2       2            1
## 4         3           2             3       2            3
## 5         2           2             1       1            1
## 6         0           0             1       0            0
## # i 50 more variables: No_home_time <dbl>, `2_strangers` <dbl>,
## #   enjoy_holiday <dbl>, enjoy_travel <dbl>, common_goals <dbl>,
## #   harmony <dbl>, freeom_value <dbl>, entertain <dbl>,
## #   people_goals <dbl>, dreams <dbl>, love <dbl>, happy <dbl>,
## #   marriage <dbl>, roles <dbl>, trust <dbl>, likes <dbl>,
## #   care_sick <dbl>, fav_food <dbl>, stresses <dbl>,
## #   inner_world <dbl>, anxieties <dbl>, ...
```

``` r
str(divorce_data)
```

```
## tibble [170 x 55] (S3: tbl_df/tbl/data.frame)
##  $ Sorry_end                    : num [1:170] 2 4 2 3 2 0 3 2 2 1 ...
##  $ Ignore_diff                  : num [1:170] 2 4 2 2 2 0 3 1 2 1 ...
##  $ begin_correct                : num [1:170] 4 4 2 3 1 1 3 2 1 1 ...
##  $ Contact                      : num [1:170] 1 4 2 2 1 0 2 2 0 1 ...
##  $ Special_time                 : num [1:170] 0 4 1 3 1 0 1 2 0 1 ...
##  $ No_home_time                 : num [1:170] 0 0 3 3 1 2 3 1 4 2 ...
##  $ 2_strangers                  : num [1:170] 0 0 2 3 0 0 4 0 1 0 ...
##  $ enjoy_holiday                : num [1:170] 0 4 1 3 0 0 3 3 3 2 ...
##  $ enjoy_travel                 : num [1:170] 0 4 1 3 0 0 2 3 3 2 ...
##  $ common_goals                 : num [1:170] 0 4 2 3 0 1 2 2 3 2 ...
##  $ harmony                      : num [1:170] 1 4 3 4 0 0 2 4 3 3 ...
##  $ freeom_value                 : num [1:170] 0 3 4 3 1 2 2 3 3 0 ...
##  $ entertain                    : num [1:170] 1 4 2 3 0 1 2 2 3 0 ...
##  $ people_goals                 : num [1:170] 1 0 3 4 1 0 3 3 3 2 ...
##  $ dreams                       : num [1:170] 0 4 3 3 1 2 2 4 3 1 ...
##  $ love                         : num [1:170] 1 4 3 3 1 0 3 3 3 0 ...
##  $ happy                        : num [1:170] 0 4 3 3 1 2 3 2 3 1 ...
##  $ marriage                     : num [1:170] 0 4 3 3 1 1 3 3 3 2 ...
##  $ roles                        : num [1:170] 0 3 3 3 2 0 3 2 3 1 ...
##  $ trust                        : num [1:170] 1 2 2 4 1 1 2 1 3 0 ...
##  $ likes                        : num [1:170] 0 1 1 1 1 0 3 2 2 0 ...
##  $ care_sick                    : num [1:170] 0 1 0 1 0 0 3 1 2 0 ...
##  $ fav_food                     : num [1:170] 0 0 1 1 0 0 3 1 2 0 ...
##  $ stresses                     : num [1:170] 0 2 2 1 0 0 3 2 3 1 ...
##  $ inner_world                  : num [1:170] 0 2 2 2 0 2 2 3 2 1 ...
##  $ anxieties                    : num [1:170] 0 1 2 1 2 2 3 3 3 1 ...
##  $ current_stress               : num [1:170] 0 2 2 1 1 0 3 2 2 1 ...
##  $ hopes_wishes                 : num [1:170] 0 0 2 1 2 0 2 2 3 1 ...
##  $ know_well                    : num [1:170] 0 1 3 1 1 0 2 2 2 1 ...
##  $ friends_social               : num [1:170] 1 1 2 3 1 0 2 3 3 1 ...
##  $ Aggro_argue                  : num [1:170] 1 0 3 2 1 4 1 1 1 1 ...
##  $ Always_never                 : num [1:170] 2 4 3 3 1 1 2 1 1 1 ...
##  $ negative_personality         : num [1:170] 1 2 1 2 1 1 2 0 1 0 ...
##  $ offensive_expressions        : num [1:170] 2 3 1 2 1 1 1 2 1 1 ...
##  $ insult                       : num [1:170] 0 0 1 1 0 1 1 2 1 0 ...
##  $ humiliate                    : num [1:170] 1 2 1 1 0 1 2 1 1 0 ...
##  $ not_calm                     : num [1:170] 2 3 2 3 0 1 3 4 1 1 ...
##  $ hate_subjects                : num [1:170] 1 4 1 3 0 2 2 4 2 1 ...
##  $ sudden_discussion            : num [1:170] 3 2 3 4 2 0 2 4 2 2 ...
##  $ idk_what's_going_on          : num [1:170] 3 4 3 4 1 2 3 4 2 2 ...
##  $ calm_breaks                  : num [1:170] 2 2 3 2 0 2 3 4 2 1 ...
##  $ argue_then_leave             : num [1:170] 1 2 3 2 2 1 3 4 2 2 ...
##  $ silent_for_calm              : num [1:170] 1 3 2 3 3 2 3 3 2 3 ...
##  $ good_to_leave_home           : num [1:170] 2 4 3 2 0 3 4 2 2 2 ...
##  $ silence_instead_of_discussion: num [1:170] 3 2 2 3 2 0 3 0 2 2 ...
##  $ silence_for_harm             : num [1:170] 2 2 3 2 2 2 3 0 1 2 ...
##  $ silence_fear_anger           : num [1:170] 1 2 2 2 1 2 2 1 1 0 ...
##  $ I'm_right                    : num [1:170] 3 3 3 3 2 1 3 2 1 2 ...
##  $ accusations                  : num [1:170] 3 4 1 3 3 2 2 2 1 2 ...
##  $ I'm_not_guilty               : num [1:170] 3 4 1 3 2 1 3 2 1 2 ...
##  $ I'm_not_wrong                : num [1:170] 2 4 1 3 2 1 3 1 1 2 ...
##  $ no_hesitancy_inadequate      : num [1:170] 3 4 2 2 2 1 2 1 1 4 ...
##  $ you're_inadequate            : num [1:170] 2 2 2 2 1 2 2 1 1 3 ...
##  $ incompetence                 : num [1:170] 1 2 2 2 0 0 2 0 1 3 ...
##  $ Divorce_Y_N                  : num [1:170] 1 1 1 1 1 1 1 1 1 1 ...
```

``` r
#Written by: Casper Collet

#A couple of variables had backticks in them and needed to be changed to ensure we can work with the dataset.

colnames(divorce_data)[colnames(divorce_data) == "2_strangers"] <- "Two_Strangers"
colnames(divorce_data)[colnames(divorce_data) == "idk_what's_going_on"] <- "idk_what_is_going_on"
colnames(divorce_data)[colnames(divorce_data) == "I'm_right"] <- "I_Am_Right"
colnames(divorce_data)[colnames(divorce_data) ==  "I'm_not_wrong"] <- "I_am_not_wrong"
colnames(divorce_data)[colnames(divorce_data) ==  "I'm_not_guilty"] <- "I_am_not_guilty"
colnames(divorce_data)[colnames(divorce_data) ==  "you're_inadequate"] <- "you_are_inadequate"

#Our first task is: Split around 20% of the dataset of so we can keep some unseen data to test our models on after we tried them on the 80%. To keep it random, we will remove the last.

set.seed(123) 
sample_index <- sample(1:nrow(divorce_data), size = round(0.2 * nrow(divorce_data)))

Unseendata <- divorce_data[sample_index, ]
seendata <- divorce_data[-sample_index, ]

table(Unseendata$Divorce_Y_N, useNA = "always") 
```

```
## 
##    0    1 <NA> 
##   21   13    0
```


``` r
#Written by: Casper Collet
#Now that we have data to work with (the remaining 80%) we can try different models to test predictability power. We start with random forest. We choos deliberatly to not split the seendata again in traindata and testdata because we have a relatively small dataset. Otherwise the machine learning might be less accurate and we don't want that.

library(randomForest)
```

```
## randomForest 4.7-1.2
```

```
## Type rfNews() to see new features/changes/bug fixes.
```

``` r
#To ensure the last variables not interfering with the tests, we make it a binary valuable with either 1 or 0 and remove the old variable. This is just to be sure.

seendata$Divorce_Y_N <- as.factor(seendata$Divorce_Y_N)

rf_model <- randomForest(Divorce_Y_N ~ ., data = seendata, ntree = 500, mtry = 3, importance = TRUE)
print(rf_model)
```

```
## 
## Call:
##  randomForest(formula = Divorce_Y_N ~ ., data = seendata, ntree = 500,      mtry = 3, importance = TRUE) 
##                Type of random forest: classification
##                      Number of trees: 500
## No. of variables tried at each split: 3
## 
##         OOB estimate of  error rate: 2.94%
## Confusion matrix:
##    0  1 class.error
## 0 65  0  0.00000000
## 1  4 67  0.05633803
```


``` r
#Written by Casper Collet
#Here we test the accuracy of the model on the unseendata, this came down to 100%, because it had perfect accuracy.
library(caret)
```

```
## 载入需要的程序包：ggplot2
```

```
## 
## 载入程序包：'ggplot2'
```

```
## The following object is masked from 'package:randomForest':
## 
##     margin
```

```
## 载入需要的程序包：lattice
```

``` r
Unseendata$Divorce_Y_N <- factor(Unseendata$Divorce_Y_N, levels = levels(seendata$Divorce_Y_N))

unseen_predictions <- predict(rf_model, Unseendata)

# Evaluate the accuracy on Unseendata
conf_matrix_unseen <- confusionMatrix(unseen_predictions, Unseendata$Divorce_Y_N)
print(conf_matrix_unseen)
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction  0  1
##          0 21  0
##          1  0 13
##                                      
##                Accuracy : 1          
##                  95% CI : (0.8972, 1)
##     No Information Rate : 0.6176     
##     P-Value [Acc > NIR] : 7.677e-08  
##                                      
##                   Kappa : 1          
##                                      
##  Mcnemar's Test P-Value : NA         
##                                      
##             Sensitivity : 1.0000     
##             Specificity : 1.0000     
##          Pos Pred Value : 1.0000     
##          Neg Pred Value : 1.0000     
##              Prevalence : 0.6176     
##          Detection Rate : 0.6176     
##    Detection Prevalence : 0.6176     
##       Balanced Accuracy : 1.0000     
##                                      
##        'Positive' Class : 0          
## 
```


``` r
#Written by: Casper Collet
#We can use this random forest also to check for the most important questions for predicting divorce, after we use the different methods we can see if they also validate these.
importance(rf_model) 
```

```
##                                         0          1
## Sorry_end                      4.35485528  3.1599413
## Ignore_diff                    3.92817159  1.5013090
## begin_correct                  4.55375850  2.5132655
## Contact                        3.03733650  1.6192854
## Special_time                   3.94192257  1.2643879
## No_home_time                   2.40746633  0.8597980
## Two_Strangers                  1.91168778  1.0010015
## enjoy_holiday                  4.89673224  1.4045198
## enjoy_travel                   5.92350917  3.1096731
## common_goals                   2.45576153  2.2186772
## harmony                        6.98802013  3.4472884
## freeom_value                   4.62187201  3.2821086
## entertain                      2.33319060  2.0613578
## people_goals                   4.82930948  2.0945149
## dreams                         4.99977916  2.4900695
## love                           5.15130943  2.4302510
## happy                          5.62677295  3.3731418
## marriage                       7.69938291  4.4383586
## roles                          6.86261160  2.2921012
## trust                          6.74383105  3.9966733
## likes                          4.23100176  0.5233748
## care_sick                      2.55662364  0.1734802
## fav_food                       1.27238870  0.9887372
## stresses                       3.11171676  1.8738516
## inner_world                    4.67540575  0.8017336
## anxieties                      7.63161757  1.7697364
## current_stress                 5.28280213  0.4854395
## hopes_wishes                   5.55311722  1.2615443
## know_well                      5.20288997  1.9590974
## friends_social                 4.18472736  1.9289411
## Aggro_argue                    3.96441646  1.1707149
## Always_never                   2.90078730  2.1588226
## negative_personality           2.91855583  2.2317355
## offensive_expressions          1.84126289  1.6576133
## insult                         4.16680482  3.2032263
## humiliate                      8.82621471  2.3761013
## not_calm                       2.78643370  1.9262824
## hate_subjects                  3.85891322  0.6844475
## sudden_discussion              7.07406410  3.6120689
## idk_what_is_going_on           7.00596029  3.1649355
## calm_breaks                    3.41225405  1.1627732
## argue_then_leave               0.05579986  0.4532879
## silent_for_calm                0.06971577  0.4707830
## good_to_leave_home             3.90391570  0.9846291
## silence_instead_of_discussion -0.03056018 -0.2305853
## silence_for_harm               0.88086032  0.2457844
## silence_fear_anger            -0.67852685  1.4075290
## I_Am_Right                     1.51872917  1.8399575
## accusations                    3.57332224  2.3888827
## I_am_not_guilty                2.63014199  0.8549387
## I_am_not_wrong                 0.88832224  0.6709801
## no_hesitancy_inadequate        3.12175001 -0.1085747
## you_are_inadequate             2.81170058  2.6415524
## incompetence                   3.02503648  1.3265087
##                               MeanDecreaseAccuracy
## Sorry_end                                4.8195959
## Ignore_diff                              3.6709555
## begin_correct                            4.9952608
## Contact                                  3.2064835
## Special_time                             4.2313999
## No_home_time                             2.5973924
## Two_Strangers                            1.9457729
## enjoy_holiday                            4.9499212
## enjoy_travel                             6.1518887
## common_goals                             3.2117794
## harmony                                  6.6907510
## freeom_value                             5.4659352
## entertain                                3.1964378
## people_goals                             4.8782374
## dreams                                   5.4273304
## love                                     5.3851690
## happy                                    5.8958177
## marriage                                 7.8288733
## roles                                    6.5051859
## trust                                    7.1292050
## likes                                    4.1623745
## care_sick                                2.5868688
## fav_food                                 1.3770981
## stresses                                 3.6166925
## inner_world                              4.8881301
## anxieties                                7.8329617
## current_stress                           5.1890326
## hopes_wishes                             5.5173929
## know_well                                5.7640432
## friends_social                           4.6472452
## Aggro_argue                              4.3603927
## Always_never                             3.3003964
## negative_personality                     3.5821743
## offensive_expressions                    2.5902318
## insult                                   4.9484221
## humiliate                                8.8001189
## not_calm                                 3.3786181
## hate_subjects                            3.9122283
## sudden_discussion                        7.4697764
## idk_what_is_going_on                     7.1254550
## calm_breaks                              3.7517058
## argue_then_leave                         0.3292612
## silent_for_calm                          0.2670836
## good_to_leave_home                       4.1518219
## silence_instead_of_discussion           -0.1006453
## silence_for_harm                         0.8390325
## silence_fear_anger                      -0.2511954
## I_Am_Right                               2.4742661
## accusations                              3.8942529
## I_am_not_guilty                          2.7796605
## I_am_not_wrong                           1.1358455
## no_hesitancy_inadequate                  2.7535608
## you_are_inadequate                       3.9435847
## incompetence                             3.2476735
##                               MeanDecreaseGini
## Sorry_end                           1.15928404
## Ignore_diff                         0.71688398
## begin_correct                       0.52637165
## Contact                             1.34455999
## Special_time                        0.99693731
## No_home_time                        0.26098912
## Two_Strangers                       0.03293901
## enjoy_holiday                       1.36066269
## enjoy_travel                        2.06887616
## common_goals                        0.41289854
## harmony                             3.40019313
## freeom_value                        2.19506443
## entertain                           0.78263249
## people_goals                        1.59886798
## dreams                              1.38323583
## love                                2.25692203
## happy                               2.95055508
## marriage                            3.91316291
## roles                               3.16718351
## trust                               3.32777368
## likes                               1.45155197
## care_sick                           0.78546085
## fav_food                            0.28975176
## stresses                            0.69888816
## inner_world                         2.02094269
## anxieties                           2.77868572
## current_stress                      2.14543224
## hopes_wishes                        1.27533589
## know_well                           1.22375101
## friends_social                      1.65163116
## Aggro_argue                         0.90292300
## Always_never                        0.94050897
## negative_personality                0.87516026
## offensive_expressions               0.70394212
## insult                              1.59486322
## humiliate                           3.35536823
## not_calm                            1.07163157
## hate_subjects                       1.20684653
## sudden_discussion                   2.35519159
## idk_what_is_going_on                2.76699455
## calm_breaks                         0.41582772
## argue_then_leave                    0.17730086
## silent_for_calm                     0.08022812
## good_to_leave_home                  0.93343546
## silence_instead_of_discussion       0.07853969
## silence_for_harm                    0.06018524
## silence_fear_anger                  0.06127762
## I_Am_Right                          0.09782898
## accusations                         0.20524112
## I_am_not_guilty                     0.13216134
## I_am_not_wrong                      0.20500486
## no_hesitancy_inadequate             0.18798842
## you_are_inadequate                  0.31730943
## incompetence                        0.44131354
```

``` r
varImpPlot(rf_model) 
```

![](DSL-FINAL-CODE_files/figure-latex/unnamed-chunk-5-1.pdf)<!-- --> 

``` r
Randomforest_most_important_questions <- importance(rf_model) #To compare later on
```


``` r
#Written by: Casper Collet
#Secondly, we will try the method Bagging (Bootstrap Aggregating). This is quite similar to RandomForest, but might give us some new insights. 

bagging_model <- randomForest(Divorce_Y_N ~ ., data = seendata, ntree = 500, mtry = ncol(seendata) - 1, importance = TRUE)

print(bagging_model)
```

```
## 
## Call:
##  randomForest(formula = Divorce_Y_N ~ ., data = seendata, ntree = 500,      mtry = ncol(seendata) - 1, importance = TRUE) 
##                Type of random forest: classification
##                      Number of trees: 500
## No. of variables tried at each split: 54
## 
##         OOB estimate of  error rate: 2.94%
## Confusion matrix:
##    0  1 class.error
## 0 65  0  0.00000000
## 1  4 67  0.05633803
```

``` r
#We immediately see that in the bagging method, has one less falsely classified object in the confusion matrix (4 became 3). Next on we test the bagging method on the unseen data. This show us an accuracy of 77.14% which is less than the 100% from random forest.

unseen_predictions <- predict(bagging_model, Unseendata)

# Evaluate the accuracy on Unseendata
conf_matrix_unseenbag <- confusionMatrix(unseen_predictions, Unseendata$Divorce_Y_N)
print(conf_matrix_unseenbag)
```

```
## Confusion Matrix and Statistics
## 
##           Reference
## Prediction  0  1
##          0 21  0
##          1  0 13
##                                      
##                Accuracy : 1          
##                  95% CI : (0.8972, 1)
##     No Information Rate : 0.6176     
##     P-Value [Acc > NIR] : 7.677e-08  
##                                      
##                   Kappa : 1          
##                                      
##  Mcnemar's Test P-Value : NA         
##                                      
##             Sensitivity : 1.0000     
##             Specificity : 1.0000     
##          Pos Pred Value : 1.0000     
##          Neg Pred Value : 1.0000     
##              Prevalence : 0.6176     
##          Detection Rate : 0.6176     
##    Detection Prevalence : 0.6176     
##       Balanced Accuracy : 1.0000     
##                                      
##        'Positive' Class : 0          
## 
```

``` r
#Here we show the most important variables from the bagging model.

importance(bagging_model)
```

```
##                                        0           1
## Sorry_end                      2.5244021  2.32136035
## Ignore_diff                    1.9147422  1.20861960
## begin_correct                  5.2602147  3.15005104
## Contact                        1.2144654  1.07054932
## Special_time                   0.0000000  0.00000000
## No_home_time                  -1.0010015  0.00000000
## Two_Strangers                  1.4159137 -1.00100150
## enjoy_holiday                  3.2700303 -1.49750575
## enjoy_travel                   5.9011361  0.91047699
## common_goals                  -1.0010015  0.00000000
## harmony                       12.4983424  2.96179617
## freeom_value                   3.3932772  2.62376540
## entertain                     -1.0010015  1.00100150
## people_goals                   1.9665137  1.56492105
## dreams                         0.0000000  0.00000000
## love                           1.0105167  2.26658637
## happy                          6.6688655  2.86219472
## marriage                      12.4401725  3.83388435
## roles                          8.7161912  2.84294155
## trust                          5.5063648  5.36087854
## likes                          1.0010015 -1.00100150
## care_sick                      0.0000000  0.00000000
## fav_food                       0.0000000  0.00000000
## stresses                       1.0010015  0.00000000
## inner_world                    2.3695214 -1.89498647
## anxieties                     14.3814287  3.23998256
## current_stress                 0.0000000  0.00000000
## hopes_wishes                   7.4888243 -4.10894220
## know_well                      1.9523560  0.02244502
## friends_social                 1.4999534  2.00449450
## Aggro_argue                    1.1617832  0.00000000
## Always_never                  -0.2934805  1.69662358
## negative_personality           1.2847447  1.97135644
## offensive_expressions          0.6392620  1.00100150
## insult                         1.3030791 -1.00100150
## humiliate                     12.9761553  2.89266071
## not_calm                       0.0000000  0.00000000
## hate_subjects                  0.0000000  0.00000000
## sudden_discussion              7.4418376  2.92181705
## idk_what_is_going_on           8.7414851  3.38849359
## calm_breaks                    1.3005304  1.32749720
## argue_then_leave               0.0000000  0.00000000
## silent_for_calm                0.0000000  0.00000000
## good_to_leave_home             2.0471027  0.60745330
## silence_instead_of_discussion  0.0000000  0.00000000
## silence_for_harm              -1.0010015 -1.00100150
## silence_fear_anger            -1.4027521  0.00000000
## I_Am_Right                     0.0000000  0.00000000
## accusations                   -1.4158171  1.22077431
## I_am_not_guilty                1.0010015  1.16474879
## I_am_not_wrong                -1.0010015  1.33046917
## no_hesitancy_inadequate        1.2633950  1.44198802
## you_are_inadequate             2.3522279  3.55110511
## incompetence                   1.6758732 -1.65167791
##                               MeanDecreaseAccuracy
## Sorry_end                                2.3921092
## Ignore_diff                              1.9808712
## begin_correct                            5.4214026
## Contact                                  1.3182261
## Special_time                             0.0000000
## No_home_time                            -1.0010015
## Two_Strangers                            1.3657069
## enjoy_holiday                            3.2619752
## enjoy_travel                             5.8731881
## common_goals                            -1.0010015
## harmony                                 11.9500940
## freeom_value                             3.6860698
## entertain                                1.0010015
## people_goals                             2.0866757
## dreams                                   0.0000000
## love                                     2.4927791
## happy                                    6.8907181
## marriage                                12.2437008
## roles                                    8.3758565
## trust                                    6.2041690
## likes                                    1.0010015
## care_sick                                0.0000000
## fav_food                                 0.0000000
## stresses                                 1.0010015
## inner_world                              2.2590322
## anxieties                               14.4891111
## current_stress                           0.0000000
## hopes_wishes                             7.5320298
## know_well                                1.9780312
## friends_social                           1.9926582
## Aggro_argue                              1.1353003
## Always_never                             1.5090190
## negative_personality                     2.2084659
## offensive_expressions                    0.7680146
## insult                                   1.2075171
## humiliate                               12.6113351
## not_calm                                 0.0000000
## hate_subjects                            0.0000000
## sudden_discussion                        7.4693606
## idk_what_is_going_on                     8.7966539
## calm_breaks                              1.6401632
## argue_then_leave                         0.0000000
## silent_for_calm                          0.0000000
## good_to_leave_home                       2.4106127
## silence_instead_of_discussion            0.0000000
## silence_for_harm                        -1.4073060
## silence_fear_anger                      -1.4145954
## I_Am_Right                               0.0000000
## accusations                              0.6614300
## I_am_not_guilty                          1.1625031
## I_am_not_wrong                           1.0010015
## no_hesitancy_inadequate                  1.9051768
## you_are_inadequate                       3.7183286
## incompetence                             1.7026633
##                               MeanDecreaseGini
## Sorry_end                          0.172549975
## Ignore_diff                        0.284430031
## begin_correct                      0.255055214
## Contact                            0.034889569
## Special_time                       0.000000000
## No_home_time                       0.003940299
## Two_Strangers                      0.011655037
## enjoy_holiday                      0.046691034
## enjoy_travel                       0.791294552
## common_goals                       0.002000000
## harmony                           11.779898310
## freeom_value                       1.818728733
## entertain                          0.003946667
## people_goals                       0.155181277
## dreams                             0.003937500
## love                               0.034527418
## happy                              5.286818014
## marriage                          11.622794883
## roles                              6.411151997
## trust                              5.601883309
## likes                              0.003937500
## care_sick                          0.002666667
## fav_food                           0.000000000
## stresses                           0.007774648
## inner_world                        0.407506055
## anxieties                          4.840330551
## current_stress                     0.000000000
## hopes_wishes                       0.267868928
## know_well                          0.147232873
## friends_social                     0.175573727
## Aggro_argue                        0.006938462
## Always_never                       0.014376662
## negative_personality               0.023569788
## offensive_expressions              0.010971429
## insult                             0.259983884
## humiliate                          8.244080529
## not_calm                           0.000000000
## hate_subjects                      0.000000000
## sudden_discussion                  2.732243293
## idk_what_is_going_on               5.431271616
## calm_breaks                        0.131096744
## argue_then_leave                   0.000000000
## silent_for_calm                    0.002666667
## good_to_leave_home                 0.170313768
## silence_instead_of_discussion      0.002666667
## silence_for_harm                   0.009857143
## silence_fear_anger                 0.007890916
## I_Am_Right                         0.005333333
## accusations                        0.015032700
## I_am_not_guilty                    0.007865308
## I_am_not_wrong                     0.010057143
## no_hesitancy_inadequate            0.018633422
## you_are_inadequate                 0.094812175
## incompetence                       0.015397113
```

``` r
varImpPlot(bagging_model)
```

![](DSL-FINAL-CODE_files/figure-latex/unnamed-chunk-6-1.pdf)<!-- --> 

``` r
Bagging_most_important_questions <- importance(bagging_model)
```


``` r
#Next up is the Lasso model (Least Absolute Shrinkage and Selection Operator). We have no categorical objects and already made sure before that the Divorce column is binary.(C.L)

# Load required packages
library(glmnet)
```

```
## Loaded glmnet 4.1-8
```

``` r
# Prepare the data for Lasso and Ridge models
# Convert the dataset to a matrix format suitable for glmnet
x <- as.matrix(seendata[, -ncol(seendata)])  # All predictor variables
y <- as.numeric(as.character(seendata$Divorce_Y_N))  # Convert factor to numeric response

# Fit Lasso model
lasso_model <- cv.glmnet(x, y, alpha = 1, family = "binomial")  # L1 regularization
lasso_best_lambda <- lasso_model$lambda.min  # Get the best lambda
lasso_coefficients <- coef(lasso_model, s = lasso_best_lambda)  # Extract coefficients
# Print results
print("Lasso Model Coefficients:")
```

```
## [1] "Lasso Model Coefficients:"
```

``` r
print(lasso_coefficients)
```

```
## 55 x 1 sparse Matrix of class "dgCMatrix"
##                                        s1
## (Intercept)                   -5.59910699
## Sorry_end                      .         
## Ignore_diff                    .         
## begin_correct                  0.31654611
## Contact                        .         
## Special_time                   .         
## No_home_time                   0.52719617
## Two_Strangers                  .         
## enjoy_holiday                  .         
## enjoy_travel                   .         
## common_goals                   .         
## harmony                        .         
## freeom_value                   .         
## entertain                      .         
## people_goals                   .         
## dreams                         .         
## love                           .         
## happy                          .         
## marriage                       0.34439551
## roles                          .         
## trust                          .         
## likes                          .         
## care_sick                      .         
## fav_food                       .         
## stresses                       .         
## inner_world                    .         
## anxieties                      0.87175183
## current_stress                 .         
## hopes_wishes                   .         
## know_well                      .         
## friends_social                 .         
## Aggro_argue                    .         
## Always_never                   .         
## negative_personality           .         
## offensive_expressions          .         
## insult                         .         
## humiliate                      .         
## not_calm                       .         
## hate_subjects                  .         
## sudden_discussion              0.16476958
## idk_what_is_going_on           1.20138456
## calm_breaks                    .         
## argue_then_leave               .         
## silent_for_calm                .         
## good_to_leave_home             .         
## silence_instead_of_discussion  .         
## silence_for_harm               .         
## silence_fear_anger             .         
## I_Am_Right                     .         
## accusations                    0.31357374
## I_am_not_guilty                .         
## I_am_not_wrong                 .         
## no_hesitancy_inadequate        0.09395887
## you_are_inadequate             .         
## incompetence                   .
```


``` r
#Last but not least, the Ridge model.(C.L)
install.packages("glmnet", dependencies = TRUE)
```

```
## Error in install.packages : Updating loaded packages
```

``` r
library(glmnet)
ridge_model <- cv.glmnet(x, y, alpha = 0, family = "binomial")  # L2 regularization
ridge_best_lambda <- ridge_model$lambda.min  # Get the best lambda
ridge_coefficients <- coef(ridge_model, s = ridge_best_lambda)  # Extract coefficients

print("Ridge Model Coefficients:")
```

```
## [1] "Ridge Model Coefficients:"
```

``` r
print(ridge_coefficients)
```

```
## 55 x 1 sparse Matrix of class "dgCMatrix"
##                                          s1
## (Intercept)                   -5.5349425462
## Sorry_end                      0.1107944775
## Ignore_diff                    0.1266043275
## begin_correct                  0.1901657103
## Contact                        0.0754199862
## Special_time                   0.0416007180
## No_home_time                   0.3199887393
## Two_Strangers                  0.0379383330
## enjoy_holiday                  0.0498611694
## enjoy_travel                   0.0573544730
## common_goals                   0.0207720760
## harmony                        0.0795070611
## freeom_value                   0.0816969259
## entertain                     -0.0134706811
## people_goals                   0.0945548559
## dreams                         0.1212478731
## love                           0.0750371448
## happy                          0.1210761220
## marriage                       0.1247041148
## roles                          0.0862251739
## trust                          0.1181211869
## likes                          0.0404806290
## care_sick                      0.0009696236
## fav_food                       0.0021058120
## stresses                       0.0042016791
## inner_world                    0.0578491198
## anxieties                      0.1740636538
## current_stress                 0.0567880585
## hopes_wishes                   0.1236773172
## know_well                      0.0612024310
## friends_social                 0.0864886501
## Aggro_argue                    0.1277342939
## Always_never                   0.0610147825
## negative_personality           0.0543815048
## offensive_expressions          0.0809120729
## insult                         0.0325045867
## humiliate                      0.0638387007
## not_calm                       0.0362930120
## hate_subjects                  0.0743739589
## sudden_discussion              0.1307811409
## idk_what_is_going_on           0.1825973655
## calm_breaks                    0.0910542506
## argue_then_leave               0.0568690904
## silent_for_calm                0.0455944138
## good_to_leave_home             0.1352975332
## silence_instead_of_discussion  0.0212942397
## silence_for_harm               0.0124038811
## silence_fear_anger             0.0105782326
## I_Am_Right                    -0.0122686690
## accusations                    0.1714810824
## I_am_not_guilty                0.0982993921
## I_am_not_wrong                 0.0175643792
## no_hesitancy_inadequate        0.1288393287
## you_are_inadequate             0.1236023416
## incompetence                   0.0164031145
```



``` r
# Evaluate 2 models (Lasso, Ridge) using Unseendata. Then calculate Accuracy, AUC-ROC curves, and Mean Square Error (MSE) for each model. Finally Visualize AUC-ROC curves to compare model performance (C.L)

# Load necessary libraries
library(glmnet)
library(pROC)
```

```
## Type 'citation("pROC")' for a citation.
```

```
## 
## 载入程序包：'pROC'
```

```
## The following objects are masked from 'package:stats':
## 
##     cov, smooth, var
```

``` r
library(caret)

# Convert Divorce label to factor for classification
Unseendata$Divorce_Y_N <- as.factor(Unseendata$Divorce_Y_N)

# Prepare data matrices for Lasso and Ridge (glmnet requires matrix input)
x_train <- as.matrix(seendata[, -ncol(seendata)])  # Features from seen data
y_train <- as.numeric(as.character(seendata$Divorce_Y_N))  # Convert factor to numeric
x_test <- as.matrix(Unseendata[, -ncol(Unseendata)])  # Features from unseen data
y_test <- as.numeric(as.character(Unseendata$Divorce_Y_N))  # Convert factor to numeric

# Train Lasso Model (L1 regularization)
lasso_model <- cv.glmnet(x_train, y_train, alpha = 1, family = "binomial")
lasso_pred <- predict(lasso_model, newx = x_test, s = "lambda.min", type = "response")
lasso_class <- ifelse(lasso_pred > 0.5, 1, 0)  # Convert probabilities to binary labels

# Train Ridge Model (L2 regularization)
ridge_model <- cv.glmnet(x_train, y_train, alpha = 0, family = "binomial")
ridge_pred <- predict(ridge_model, newx = x_test, s = "lambda.min", type = "response")
ridge_class <- ifelse(ridge_pred > 0.5, 1, 0)  # Convert probabilities to binary labels

# Compute evaluation metrics
evaluate_model <- function(true_labels, predicted_labels, predicted_probs) {
  accuracy <- sum(true_labels == predicted_labels) / length(true_labels)  # Compute accuracy
  auc <- auc(roc(true_labels, predicted_probs))  # Compute AUC-ROC
  mse <- mean((true_labels - predicted_probs)^2)  # Compute Mean Squared Error
  return(list(accuracy = accuracy, AUC = auc, MSE = mse))
}

# Evaluate Lasso
lasso_results <- evaluate_model(y_test, lasso_class, lasso_pred)
```

```
## Setting levels: control = 0, case = 1
```

```
## Warning in roc.default(true_labels, predicted_probs): Deprecated
## use a matrix as predictor. Unexpected results may be produced,
## please pass a numeric vector.
```

```
## Setting direction: controls < cases
```

``` r
print("Lasso Model Results:")
```

```
## [1] "Lasso Model Results:"
```

``` r
print(lasso_results)
```

```
## $accuracy
## [1] 1
## 
## $AUC
## Area under the curve: 1
## 
## $MSE
## [1] 0.0007408773
```

``` r
# Evaluate Ridge
ridge_results <- evaluate_model(y_test, ridge_class, ridge_pred)
```

```
## Setting levels: control = 0, case = 1
```

```
## Warning in roc.default(true_labels, predicted_probs): Deprecated
## use a matrix as predictor. Unexpected results may be produced,
## please pass a numeric vector.
```

```
## Setting direction: controls < cases
```

``` r
print("Ridge Model Results:")
```

```
## [1] "Ridge Model Results:"
```

``` r
print(ridge_results)
```

```
## $accuracy
## [1] 1
## 
## $AUC
## Area under the curve: 1
## 
## $MSE
## [1] 0.001368812
```

``` r
# Plot AUC-ROC Curves
roc_lasso <- roc(y_test, lasso_pred)
```

```
## Setting levels: control = 0, case = 1
```

```
## Warning in roc.default(y_test, lasso_pred): Deprecated use a
## matrix as predictor. Unexpected results may be produced, please
## pass a numeric vector.
```

```
## Setting direction: controls < cases
```

``` r
roc_ridge <- roc(y_test, ridge_pred)
```

```
## Setting levels: control = 0, case = 1
```

```
## Warning in roc.default(y_test, ridge_pred): Deprecated use a
## matrix as predictor. Unexpected results may be produced, please
## pass a numeric vector.
```

```
## Setting direction: controls < cases
```

``` r
plot(roc_lasso, col = "blue", main = "AUC-ROC Curves for Lasso and Ridge")
plot(roc_ridge, col = "red", add = TRUE)
legend("bottomright", legend = c("Lasso", "Ridge"), col = c("blue", "red"), lty = 1)
```

![](DSL-FINAL-CODE_files/figure-latex/unnamed-chunk-9-1.pdf)<!-- --> 


``` r
# Load necessary libraries
library(randomForest)
library(pROC)
library(caret)

# Convert Divorce label to factor for classification
colnames(Unseendata)[colnames(Unseendata) == "Divorced"] <- "Divorce_Y_N"
Unseendata$Divorce_Y_N <- as.factor(Unseendata$Divorce_Y_N)

# Train Random Forest Model
rf_model <- randomForest(Divorce_Y_N ~ ., data = seendata, ntree = 500, mtry = 3, importance = TRUE)
rf_pred <- predict(rf_model, newdata = Unseendata, type = "prob")[,2]  # Extract probability scores
rf_class <- ifelse(rf_pred > 0.5, 1, 0)  # Convert probabilities to binary labels

# Train Bagging Model
bagging_model <- randomForest(Divorce_Y_N ~ ., data = seendata, ntree = 500, mtry = ncol(seendata) - 1, importance = TRUE)
bagging_pred <- predict(bagging_model, newdata = Unseendata, type = "prob")[,2]
bagging_class <- ifelse(bagging_pred > 0.5, 1, 0)

# Function to compute evaluation metrics
evaluate_model <- function(true_labels, predicted_labels, predicted_probs) {
  accuracy <- sum(true_labels == predicted_labels) / length(true_labels)  # Compute accuracy
  auc <- auc(roc(true_labels, predicted_probs))  # Compute AUC-ROC
  mse <- mean((true_labels - predicted_probs)^2)  # Compute Mean Squared Error
  return(list(accuracy = accuracy, AUC = auc, MSE = mse))
}

# Evaluate Random Forest
rf_results <- evaluate_model(as.numeric(as.character(Unseendata$Divorce_Y_N)), rf_class, rf_pred)
```

```
## Setting levels: control = 0, case = 1
```

```
## Setting direction: controls < cases
```

``` r
print("Random Forest Model Results:")
```

```
## [1] "Random Forest Model Results:"
```

``` r
print(rf_results)
```

```
## $accuracy
## [1] 1
## 
## $AUC
## Area under the curve: 1
## 
## $MSE
## [1] 0.004263529
```

``` r
# Evaluate Bagging
bagging_results <- evaluate_model(as.numeric(as.character(Unseendata$Divorce_Y_N)), bagging_class, bagging_pred)
```

```
## Setting levels: control = 0, case = 1
## Setting direction: controls < cases
```

``` r
print("Bagging Model Results:")
```

```
## [1] "Bagging Model Results:"
```

``` r
print(bagging_results)
```

```
## $accuracy
## [1] 1
## 
## $AUC
## Area under the curve: 1
## 
## $MSE
## [1] 0.007693412
```

``` r
# Plot AUC-ROC Curves
roc_rf <- roc(as.numeric(as.character(Unseendata$Divorce_Y_N)), rf_pred)
```

```
## Setting levels: control = 0, case = 1
## Setting direction: controls < cases
```

``` r
roc_bagging <- roc(as.numeric(as.character(Unseendata$Divorce_Y_N)), bagging_pred)
```

```
## Setting levels: control = 0, case = 1
## Setting direction: controls < cases
```

``` r
plot(roc_rf, col = "blue", main = "AUC-ROC Curves for Random Forest and Bagging")
plot(roc_bagging, col = "red", add = TRUE)
legend("bottomright", legend = c("Random Forest", "Bagging"), col = c("blue", "red"), lty = 1)
```

![](DSL-FINAL-CODE_files/figure-latex/unnamed-chunk-10-1.pdf)<!-- --> 




