Tuan Syazana Tuan Ab Rashid
Lab 12 - due April 25,2016
Selectivity patterns of mass extinctions

> 20/20

## Problem Set 1

There is a longstanding story that Triassic Diapsids outcompeted Triassic Syanpsids. Let's see if Triassic Diapsids were more likley to survive the Traissic/Jurassic extinction than Synapsids.

Question 1

Download four data sets from the paleobiology database. First, a dataset of Anisian-Rhaetian Synapsids, name it TriassicSynapsids. Second, a dataset of Anisian-Rhaetian Diapsids, name it TriassicDiapsids. Third, a dataset of post-Triassic Diapsids, name it JurassicDiapsids. Fourth, a dataset of post-Triassic Synapsids, name it JurassicSynapsids. Show your code.

````R
> TriassicSynapsids<-downloadPBDB("Synapsida","Anisian","Rhaetian")
> TriassicDiapsids<-downloadPBDB("Diapsida","Anisian","Rhaetian")
> JurassicDiapsids<-downloadPBDB("Diapsida","Jurassic","Neogene")
> JurassicSynapsids<-downloadPBDB("Synapsida","Jurassic","Neogene")
````

Question 2

````R
> TriassicSynapsids<-cleanRank(TriassicSynapsids,"genus")
> TriassicDiapsids<-cleanRank(TriassicDiapsids,"genus")
> JurassicDiapsids<-cleanRank(JurassicDiapsids,"genus")
> JurassicSynapsids<-cleanRank(JurassicSynapsids,"genus")
````

How many Diapsid genera were there in the Triassic dataset? 

````R
> TriassicDiapsids<-unique(TriassicDiapsids[,"genus"])
> length(TriassicDiapsids)
[1] 389
````

How many Synapsid genera? Show your code.

````R
> TriassicSynapsids<-unique(TriassicSynapsids[,"genus"])
> length(TriassicSynapsids)
[1] 116
````

Question 3

How many Triassic Diapsid genera survived the Triassic/Jurassic transition? How many were victiims? 

````R
> TJDiapsidSurvivors<-intersect(TriassicDiapsids,unique(JurassicDiapsids[,"genus"]))
> length(TJDiapsidSurvivors)
[1] 37
> TJDiapsidVictims<-setdiff(TriassicDiapsids,unique(JurassicDiapsids[,"genus"]))
> length(TJDiapsidVictims)
[1] 352
````

How many Triassic Synapsid genera surivived the Triassic/Jurassic Transition? How many were victims?

````R
> TJSynapsidSurvivors<-intersect(TriassicSynapsids,unique(JurassicSynapsids[,"genus"]))
> length(TJSynapsidSurvivors)
[1] 9
> TJSynapsidVictims<-setdiff(TriassicSynapsids,unique(JurassicSynapsids[,"genus"]))
> length(TJSynapsidVictims)
[1] 107
````

Question 4

Calculate the odds ratio and log-odds that Diapsid genera were more likely to survive the T/J transition than Synapsids

````R
# The odds of Diapsid survival
DiapsidSurviveOdds<- (length(TJDiapsidSurvivors)/length(TriassicDiapsids)) / (length(TJDiapsidVictims)/length(TriassicDiapsids))

# The odds of Synapsid survival
SynapsidSurviveOdds<- (length(TJSynapsidSurvivors)/length(TriassicSynapsids)) / (length(TJSynapsidVictims)/length(TriassicSynapsids))

# Find the final odds ratio
OddsRatio<- DiapsidSurviveOdds / SynapsidSurviveOdds
> OddsRatio
[1] 1.249684
> log(OddsRatio)
[1] 0.222891
````

Question 5

Using a 95% confidence interval, can you say that this odds/ratio is "statistically significant"? Show your code.

````R
# Find the Standard Error
> StandardError<-sqrt(1/length(TJDiapsidSurvivors) + 1/length(TJDiapsidVictims) + 1/length(TJSynapsidSurvivors) + 1/length(TJSynapsidVictims))
> StandardError
[1] 0.3877175

# Find the Upper 95% Confidence limit
> UpperLimit<-log(OddsRatio) + (StandardError*1.96)
> UpperLimit
[1] 0.9828172

# Find lower Upper 95% confidence limit
> LowerLimit<-log(OddsRatio) - (StandardError*1.96)
> LowerLimit
[1] -0.5370353
````

This result is not "statistically significant" because the Lower Limit of this confidence interval is negative.

## Problem Set 2

Let's apply the technique that you just learned the Triassic and Jurassic Diapsids and Synapsids.

Question 1

Download a dataset of Anisian-Rhaetian Diapsids and Synapsids, and a dataset of post-Triassic Diapsids and Synapsids. Show your code.

````R
> TriassicDS<-downloadPBDB(c("Diapsida","Synapsida"),"Anisian","Rhaetian")
> JurassicDS<-downloadPBDB(c("Diapsida","Synapsida"),"Jurassic","Neogene")

> TriassicDS<-cleanRank(TriassicDS,"genus")
> JurassicDS<-cleanRank(JurassicDS,"genus")
````

Question 2

Find the mean latitude of each genus's occurrences in your Triassic dataset. Show your code.

````R
> TriassicMeanLatitudes<-tapply(TriassicDS[,"paleolat"],TriassicDS[,"genus"],mean)
> head(TriassicMeanLatitudes)
 Acaenasuchus  Acallosuchus Acompsosaurus   Actiosaurus Adamanasuchus Adelobasileus 
       10.116        10.430        10.740        32.120        10.145        10.170 

Question 3

Find which Triassic genera were survivors and which were victims of the Triassic/Jurassic event. Show your code.

# Find the Survivors

> TriassicSurvivors<-subset(TriassicDS,TriassicDS[,"genus"]%in%unique(JurassicDS[,"genus"])==TRUE)
> TriassicSurvivors<-unique(TriassicSurvivors[,"genus"])
> head(TriassicSurvivors)
[1] "Clevosaurus"        "Grallator"          "Rhynchosauroides"   "Rotodactylus"      
[5] "Brachychirotherium" "Coelurosaurichnus"      

# Find the Victims
> TriassicVictims<-subset(TriassicDS,TriassicDS[,"genus"]%in%unique(JurassicDS[,"genus"])!=TRUE)
> TriassicVictims<-unique(TriassicVictims[,"genus"])
> head(TriassicVictims)
[1] "Icarosaurus"      "Rutiodon"         "Kuehneosuchus"    "Kuehneosaurus"    "Trilophosaurus"  
[6] "Diphydontosaurus"
````

Question 4

Find which genera of your Triassic dataset were Diapsids and which were Synapsids. Show your code.

````R
TriassicOnlyDiapsids<-subset(TriassicDS,TriassicDS[,"genus"]%in%unique(TriassicDiapsids[,"genus"])==TRUE)
TriassicOnlySynapsids<-subset(TriassicDS,TriassicDS[,"genus"]%in%unique(TriassicSynapsids[,"genus"])==TRUE)
````

Question 5

Perform a logistic regression where the outcome variable is Survivor/Victim and the input variable is the mean latitude of each genus. Show your code. Was the mean latitude of a Triassic genus a good predictor of its survival across the T/J extinction?

````R
> PTVictims<-array(0,dim=length(TriassicVictims),dimnames=list(TriassicVictims))
> head(PTVictims)
     Icarosaurus         Rutiodon    Kuehneosuchus    Kuehneosaurus   Trilophosaurus Diphydontosaurus 
               0                0                0                0                0                0 

> FinalMatrix<-merge(TriassicMeanLatitudes,PTVictims,all=TRUE,by="row.names")
> 
> head(FinalMatrix)
      Row.names      x y
1  Acaenasuchus 10.116 0
2  Acallosuchus 10.430 0
3 Acompsosaurus 10.740 0
4   Actiosaurus 32.120 0
5 Adamanasuchus 10.145 0
6 Adelobasileus 10.170 0
> 

> FinalMatrix<-transform(FinalMatrix,row.names=Row.names,Row.names=NULL)
> colnames(FinalMatrix)<-c("MeanLatitudes","Survivor/Victim")
> head(FinalMatrix)
              MeanLatitudes Survivor/Victim
Acaenasuchus         10.116               0
Acallosuchus         10.430               0
Acompsosaurus        10.740               0
Actiosaurus          32.120               0
Adamanasuchus        10.145               0
Adelobasileus        10.170               0

> FinalMatrix[is.na(FinalMatrix[,"Survivor/Victim"]),]<-1
> head(FinalMatrix)
              MeanLatitudes Survivor/Victim
Acaenasuchus         10.116               0
Acallosuchus         10.430               0
Acompsosaurus        10.740               0
Actiosaurus          32.120               0
Adamanasuchus        10.145               0
Adelobasileus        10.170               0

> Regression1<-glm(FinalMatrix[,"Survivor/Victim"]~FinalMatrix[,"MeanLatitudes"],family="binomial")
> summary(Regression1)

Call:
glm(formula = FinalMatrix[, "Survivor/Victim"] ~ FinalMatrix[, 
    "MeanLatitudes"], family = "binomial")

Deviance Residuals: 
    Min       1Q   Median       3Q      Max  
-0.4474  -0.4411  -0.4385  -0.4308   2.1889  

Coefficients:
                                 Estimate Std. Error z value Pr(>|z|)    
(Intercept)                    -2.3009122  0.1547326  -14.87   <2e-16 ***
FinalMatrix[, "MeanLatitudes"]  0.0007725  0.0051555    0.15    0.881    
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

(Dispersion parameter for binomial family taken to be 1)

    Null deviance: 308.10  on 504  degrees of freedom
Residual deviance: 308.08  on 503  degrees of freedom
AIC: 312.08

Number of Fisher Scoring iterations: 5

Was the mean latitude of a Triassic genus a good predictor of its survival across the T/J extinction?

For every one degree increase in the latitude of the genus, its (log) odds of having survived the P/T event increases by 0.0007725. Yes, the mean latitude of a Triassic genus is a good predictor of its survival across the T/J extinction.
````

Extra Credit (6 Points)

Perform a multiple logistic regression where the outcome variable is Survivor/Victim status and the input variables are the mean latitude of each genus and whether the gneus is a Diapsid/Synapsid. Is status as a Synapsid/Diapsid more or less important average paleolatitude of occurrences for survival? Show your code.

Hint:

The general formula for a multiple logistic regression is: glm(Outcome ~ Variable1 + Variable2,family="binomial")
You'll want to represent Diapsids and Synapsids with 1s and 0s, similarly to how we did survivor and victim status
