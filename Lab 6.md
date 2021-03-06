> 20/20

Tuan Syazana Tuan Ab Rashid
Lab 6

## Problem Set 1
1) As part of our matching procedure between the Macrostrat database and the Paleobiology database, we lost some data - i.e., there was some Paleobiology Database occurrences that could not be matched to the Macrostrat database. How many occurrences were lost? Show your code.

````R
> dim(DataPBDB) - dim(MacroPBDB)
[1] 25153    13
````

2) Using what you know about the Macrostrat database can you speculate as to why so much data was lost?

Because Macrostrat's coverage is currently limited to only North America.

## Problem Set 2

1) A good candidate for classification as a lagerstätten should have high diversity of different taxnomic orders. Calculate the order-level richness of each stratigraphic formation. Find the top 10 candidate units by this criteria. State them and give the code you used. Also, create a character vector( ) listing the names of these stratigraphic units. Name this vector CandidateUnits.

````R
> RichnessOrderMatrix<-specnumber(OrderMatrix)
> sortRichnessOrderMatrix<-sort(RichnessOrderMatrix)
> tail(sortRichnessOrderMatrix, n=10)
      Forteau Fm     Parker Slate   Snowy Range Fm      Weymouth Fm      Langston Fm    Wheeler Shale 
              14               16               16               16               17               18 
Marjum Limestone       Stephen Fm       Kinzers Fm       Chancellor 
              19               23               24               27 

> CandidateUnits<-names(tail(sortRichnessOrderMatrix, n=10))
> CandidateUnits
 [1] "Forteau Fm"       "Parker Slate"     "Snowy Range Fm"   "Weymouth Fm"      "Langston Fm"     
 [6] "Wheeler Shale"    "Marjum Limestone" "Stephen Fm"       "Kinzers Fm"       "Chancellor"      
````

2) A good candidate for classification as a lagerstätten should have a large number of genera that are relatively rare. Using the GenusMatrix column to find out how many samples each genus occurs in. Show the code you used. Name your output GenusFrequencies.

````R
> GenusFrequencies<-apply(GenusMatrix,2,sum)
````

3) What is the necessary code to make a frequency barplot of the GenusFrequencies?

````R
freqtable<-table(GenusFrequencies)
barplot(freqtable)
````

4) After looking at this barplot, you should see a familiar paleobiological pattern. What do we call this type of curved distribution in paleobiology and ecology. [Hint: Think back to the lectures]

Hollow curve

5) Subset your new vector GenusFrequences so that only those genera from the lower 50% of the distribution are present. In other words genera with occurrences <= to the median( ). Show your code. Name this new subset vector as RareGenera.

````R
> median(GenusFrequencies)
[1] 2
> RareGenera1<- which(GenusFrequencies <= 2)
> RareGenera<-GenusFrequencies[RareGenera1]
````

## Problem Set 3

1) Subset GenusMatrix so that it only shows the 10 stratigraphic units we determined were potential candidates. Show your code and name your new matrix, CandidateMatrix.

````R
> CandidateMatrix<-GenusMatrix[CandidateUnits, ]
````

2) Based on the output of PercentShared and your answer to Problem Set 2 - Question 1 - i.e., the ranking of candidate units based on the number of orders represented, which four units do you think are most likely to qualify as Lagerstätten? Explain your reasoning.

````R
> PercentShared<-apply(CandidateMatrix,1,percentRare,RareGenera)
> PercentShared
      Forteau Fm     Parker Slate   Snowy Range Fm      Weymouth Fm      Langston Fm    Wheeler Shale Marjum Limestone       Stephen Fm 
       0.5652174        0.2812500        0.1951220        0.6764706        0.1632653        0.2307692        0.3559322        0.3055556 
      Kinzers Fm       Chancellor 
       0.2586207        0.5714286 
````

Weymouth Fm, Chancellor, Wheeler Shale, and Marjum Limestone because they have the larger values and also a high diversity of different taxonomic orders.

3) Look closer into the into the four units you chose - using Google and information in the Paleobiology Database. One of these should be a very famous Lagerstätten. Which one? What is famous about it? What is its significance to Paleobiology?

The Chancellor Group; it includes the Burgess Shale which is significant for its location next to what was the western edge of the continental platform 505 million years ago. The sediments were deposited on the sea floor in front of this continental edge, now called the Cathedral Escarpment.
