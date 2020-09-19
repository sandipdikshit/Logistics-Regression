library(readxl)
> library(forecast)
> library(caTools)
> set.seed(123)
> A = Connect_Mobile_Attrition_Data_file
> split_A = sample.split(A$active_cust,SplitRatio = 0.8)
> Train_A=subset(A,split_A==TRUE)
> Test_A=subset(A,split_A==FALSE)
> REG = glm(Train_A$active_cust~., data = Train_A, family = "binomial")
> summary(REG)
> logit.reg.pred = predict(REG, Test_A, type = "response")
> data.frame(actual = Test_A$active_cust, predicted = logit.reg.pred)
> table(ActualValue = Test_A$active_cust, PredictedValue=logit.reg.pred>0.5)
accuracy = sum(5767,9973)/sum(5767,2661,1599,9973)
> accuracy
[1] 0.787
> error = 1 - accuracy
> error
[1] 0.213
> TP = 9973/ sum(1599,9973)
> TP
[1] 0.8618216
> FP = 2661/sum(5767,2661)
> FP
[1] 0.3157333
> specificity = 5767 / sum(5767,2661) 
> specificity 
[1] 0.6842667
> PRecision = TP/sum(2661,9973)
> PRecision
[1] 6.821447e-05
> Prevalence = sum(1599,9973)/sum(5767,2661,1599,9973)
> Prevalence
[1] 0.5786

