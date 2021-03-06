Tuan Syazana Tuan Ab Rashid
Lab 7 - due March 14, 2016

> 17/20

## Problem Set 1

1) What do the max_ma and min_ma columns of DataPBDB represent? If you do not intuitively know, you can always check the Paleobiology Database API documentation.

max_ma represents records whose temporal locality is at most this old, specified in Ma.

min_ma represents records whose temporal locality is at least this old, specified in Ma.

2) What is oldest age of each genus? [Hint: Use the tapply( ) and max( ) functions we've used in previous labs]. Show the code you would use to find out.

`> tapply(DataPBDB[,"max_ma"],DataPBDB[,"genus"],max)`

3) What is the youngest age of each genus? [Hint: Use the tapply( ) and min( ) functions we've used in previous labs]. Show the code you would use to find out.

`> tapply(DataPBDB[,"min_ma"],DataPBDB[,"genus"],min)`

4) Find which genus has the most occurrences in the dataset [Hint: Use the table( ) function!]. What code did you use?
````R
> sort(table(DataPBDB[,"genus"]))
> # anadara has the most occurrences in the dataset
````

5) What is the stratigraphic range of this taxon (i.e., your answer to question 4). Show your code.

````R
> #first occurance and last occurance of anadara
> Anadara<-DataPBDB[which(DataPBDB[,26]=="Anadara"),]
> max(Anadara[,15])
[1] 66
> min(Anadara[,16])
[1] 0
````

## Problem Set 2

1) Qualitatively describe what is happening in the following line of code. A good answer should identify what the different arguments are for each function, and what they are used for.

`mean(sample(Lucina[,"paleolng"],length(Lucina[,"paleolng"]),replace=TRUE))`

mean(): Generic function for the (trimmed) arithmetic mean.
sample(x, size, replace=TRUE): takes a sample (generates a random permutation) of the specified size (length(Lucina[,"paleolng"])) from the elements of x (Lucina) using either with or without replacement.

x: Either a vector of one or more elements from which to choose, or a positive integer.
size: a non-negative integer giving the number of items to choose.
replace=TRUE: to allow repeated elements in the sample
sample .

2) Plot a kernel density graph of ResampledMeans. Show your code. Does the distribution look approximately Gaussian? Explain why you think it does or does not.
````R
> plot(ResampledMeans)
> # No, it does not have a Gaussian distribution. The distribution is scattered and is not like a bell curve.
````

> You did not use the `density( )` function, which is why this came out incorrectly. -1 Points.

3) Find the mean of ResampledMeans, is it similar to the mean of the original data?

````R
> mean(ResampledMeans)
[1] 24.16227
Yes, it's similar.
````

4) Sort ResampledMeans from lowest to highest. [Hint: We learned how to sort a vector in Lab 6].

`> sort(ResampledMeans)`

5) Now that you have sorted ResampledMeans, what is the 2.5th percentile of ResampledMeans and what is the 97.5th percentile of Resampled means. If you do not know what a percentile is, or how to calculate it, you can use google. Show your code.

````R
> quantile(sortResampledMeans, 0.025)
    2.5% 
21.82094 
> quantile(sortResampledMeans, 0.975)
  97.5% 
26.2863 
````

6) Incidentally, these numbers (your answer to question 5) are the lower and upper confidence interval of the mean! Qualitatively explain why this is the case.

The mean should be within the lower and upper confidence interval. The boundary represents the most extreme cases of both ends.

> This is a vague answer. -0.5 points

## Problem Set 3

1) Based on the confidence intervals given above, do you think it likely or unlikely that Lucina is still alive?

Likely, since it has a negative occurance.

2) Find the extinction confidence interval for the genus Dallarca. Show your code.

````R
> Dallarca<-subset(DataPBDB,DataPBDB[,"genus"]=="Dallarca")
> estimateExtinction(Dallarca[,"min_ma"],0.95)
Earliest   Latest 
 2.58800 -3.88749 
````

3) A pure reading of the fossil record says that Dallarca went extinct at the end of the Pliocene Epoch. Based on its confidence interval, do you think it is possible that Dallarca is still extant (alive)?

Yes, since it has a negative occurance.

4) In this case, should we trust the confidence interval or a pure reading of the fossil record? Explain your reasoning.

No. It assumes randomly distributed fossils. In other words, the fossil occurrences of taxa are randomly distributed in time, and the likelihood of preservation does not change up or down a stratigraphic section.

## Problem Set 4

1) State one ecological reason why this assumption is unlikey to be true.

The fossil occurrences of taxa are not randomly distributed in time, they have more likely to occur within their own ecological niche environments

2) State one geological reason why this assumpiton is unlikely to be true.

 The likelihood of preservation does change up or down a stratigraphic section depending on a lot of factors.

> Like what? This is not a very completel answer. -0.5 points

## Problem Set 5

1) How many occurrences are in DataPBDB. How many are in ExtantData? How many occurrences were lost by limiting our anaysis to only extant bivalves?

````R
> dim(DataPBDB)
[1] 67618    26
> dim(ExtantData)
[1] 59097    26
> dim(DataPBDB)-dim(ExtantData)
[1] 8521    0
````

2) How many unique( ) genera were in DataPBDB and ExtantData, respectively. Using this information, what percentage of Cenozoic bivalves in the PBDB are still extant today.

````R
> sum(DataPBDB[,"genus"] != 0)
[1] 67618
> sum(ExtantData[,"genus"] != 0)
[1] 59097
> ((sum(DataPBDB[,"genus"] != 0)-sum(ExtantData[,"genus"] != 0))/sum(DataPBDB[,"genus"] != 0))*100
[1] 12.60167
> # 12.60167% of Cenozoic bivalves in the PBDB are still extant today
````

> This is incorrect. the answer is about 52% -1 Points

3) Find the stratigraphic range of fossil occurrences for each genus in the ExtantData dataset. If you do not remember how to do this, revisit Problem Set 1 of this lab.

`> tapply(ExtantData[,"max_ma"],ExtantData[,"genus"],max)-tapply(ExtantData[,"min_ma"],ExtantData[,"genus"],min)`

4) Using your answer to question 3, find which genera in ExtantData are not extant according to the PBDB - i.e., do not have a minimum min_age of zero. Show your code.

````R
> ExtantMin<-tapply(ExtantData[,"min_ma"],ExtantData[,"genus"],min)
> which(ExtantMin >0)
````

5) Calculate the confidence interval for the extinction of the following genera (careful with your spelling!): Scrobicularia, Meiocardia, Dimya, Digitaria, Cuspidaria, Arctica, Aloides, Kurtiella, Gouldia, and Acrosterigma. Show your code. What percentage of these taxa have confidence intervals indicating that the taxon might still be extant?

````R
> Scrobicularia<-subset(DataPBDB,DataPBDB[,"genus"]=="Scrobicularia")
> Meiocardia<-subset(DataPBDB,DataPBDB[,"genus"]=="Meiocardia")
> Dimya<-subset(DataPBDB,DataPBDB[,"genus"]=="Dimya")
> Digitaria<-subset(DataPBDB,DataPBDB[,"genus"]=="Digitaria")
> Cuspidaria<-subset(DataPBDB,DataPBDB[,"genus"]=="Cuspidaria")
> Arctica<-subset(DataPBDB,DataPBDB[,"genus"]=="Arctica")
> Aloides<-subset(DataPBDB,DataPBDB[,"genus"]=="Aloides")
> Kurtiella<-subset(DataPBDB,DataPBDB[,"genus"]=="Kurtiella")
> Gouldia<-subset(DataPBDB,DataPBDB[,"genus"]=="Gouldia")
> Acrosterigma<-subset(DataPBDB,DataPBDB[,"genus"]=="Acrosterigma")

> estimateExtinction(Scrobicularia[,"min_ma"],0.95)
 Earliest    Latest 
  0.01170 -34.70966 
> estimateExtinction(Meiocardia[,"min_ma"],0.95)
 Earliest    Latest 
 0.011700 -5.329574 
> estimateExtinction(Dimya[,"min_ma"],0.95)
 Earliest    Latest 
 0.781000 -2.054688 
> estimateExtinction(Digitaria[,"min_ma"],0.95)
 Earliest    Latest 
 0.781000 -3.761154 
> estimateExtinction(Cuspidaria[,"min_ma"],0.95)
 Earliest    Latest 
2.5880000 0.7771965 
> estimateExtinction(Arctica[,"min_ma"],0.95)
 Earliest    Latest 
 0.011700 -1.799104 
> estimateExtinction(Aloides[,"min_ma"],0.95)
Earliest   Latest 
   5.333     -Inf 
> estimateExtinction(Kurtiella[,"min_ma"],0.95)
 Earliest    Latest 
  0.01170 -34.70966 
> estimateExtinction(Gouldia[,"min_ma"],0.95)
 Earliest    Latest 
 0.011700 -2.047386 
> estimateExtinction(Acrosterigma[,"min_ma"],0.95)
 Earliest    Latest 
 0.011700 -3.481128 
````

> #90% of these taxa might still be extant.

