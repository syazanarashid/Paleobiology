Tuan Syazana Tuan Ab Rashid
Lab 4 - Due Feb 22, 2016

20/20

## Problem Set I

1) How many unique genera are in the Miocene, Early Jurasic, Late Cretaceous, and Pennsylvanian epochs (not total, each)? What code did you use to find out?

>dim(PresencePBDB)
[1] 29 903

# unique genera in Miocene
> sum(PresencePBDB[21,1:903]==1)
[1] 603

# unique genera in Early Jurassic
> sum(PresencePBDB[29,1:903]==1)
[1] 84

# unique genera in Late Cretaceous
> sum(PresencePBDB[16,1:903]==1)
[1] 375

# unique genera in Pennsylvanian
> sum(PresencePBDB[1,1:903]==1)
[1] 133

2) How many geologic epochs in general are in this dataset? What code did you use to find out?

# 29 geologic epochs
>dim(PresencePBDB)
[1] 29 903

3) Which epochs contain specimens of the genus Mytilus? What code did you find out.

> PresencePBDB[,"Mytilus"]
    Pennsylvanian  Early Ordovician Middle Ordovician   Late Ordovician        Llandovery           Wenlock            Ludlow           Pridoli     Mississippian 
                0                 0                 0                 0                 0                 0                 0                 1                 0 
   Early Devonian   Middle Devonian     Late Devonian        Cisuralian     Late Jurassic            Eocene   Late Cretaceous  Early Cretaceous   Middle Jurassic 
                1                 0                 0                 1                 1                 1                 1                 1                 1 
        Paleocene         Oligocene           Miocene    Early Jurassic       Pleistocene       Guadalupian   Middle Triassic     Late Triassic          Pliocene 
                1                 1                 1                 1                 1                 0                 1                 1                 1 
        Lopingian    Early Triassic 
                0                 1 

#epochs containing the genus Mytilus

> which((PresencePBDB[ ,"Mytilus"]) ==1)
         Pridoli   Early Devonian       Cisuralian    Late Jurassic           Eocene  Late Cretaceous Early Cretaceous  Middle Jurassic        Paleocene        Oligocene 
               8               10               13               14               15               16               17               18               19               20 
         Miocene   Early Jurassic      Pleistocene  Middle Triassic    Late Triassic         Pliocene   Early Triassic 
              21               22               23               25               26               27               29 

4) Look at the epochs in the geologic timescale. Using your answer to question 3, in which epochs can we infer that Mytilus was present, even though we have no record of them in the Paleobiology Database? How did you deduce this?

Present in all epochs from Pridoli to Pleistocene. If the Mytilus was present in two separate epochs, we can infer that it was also present during the missing time in between. The Mytilus would not have had gone through extinction and then reappear at a later time. The absence of its record in the Paleobiology Database may be due to preservation issues or insufficient data. 

# Problem Set II

1) Using your own custom R code, find the Jaccard similarity of the Pleistocene and Miocene "samples" in your PresencePBDB matrix. It is possible to code this entirely using only functions discussed in the R Tutorial. The key is to use apply( ), sum( ), table( ), and judicious use of matrix subscriptng.

S=a/(a+b)
a=number of species common to Miocene and Pleistocene
b=number of species unique to Miocene + number of species unique to Pleistocene

> MiocenePleistocenerow<-PresencePBDB[c(21,23), ]
> MiocenePleistocenebothtrue<-which(apply(MiocenePleistocenerow,2,sum) == 2)
> length(MiocenePleistocenebothtrue)
[1] 510

> MiocenePleistoceneroweither1<-which(apply(MiocenePleistocenerow,2,sum) == 1)
> length(MiocenePleistoceneroweither1)
[1] 106

> a<-length(MiocenePleistocenebothtrue)
> b<-length(MiocenePleistoceneroweither1)
> S<-a/(a+b)
> S
[1] 0.8279221

2) How can you convert your similarity index into a distance?

> 1-S
[1] 0.1720779

3) Install and load the vegan package into R. Read the help file for the vegdist function - ?vegdist or help(vegdist). You must have already loaded the vegan package in order for it to run.

Again, calculate the jaccard distance of the "Miocene" and "Pleistocene" samples of PresencePBDB, but this time use the vegdist( ) function. This should be an identical answer to what you got in question 2. [Hint: You will have to change one of the default settings of the function]

> vegdist(PresencePBDB[c(21,23),1:903], method="jaccard", binary=FALSE, na.rm=FALSE)
              Miocene
Pleistocene 0.1720779

4) Using the vegdist( ) function. Calculate the Jaccard distances of all the following epochs in PresencePBDB - the "Pleistocene", "Pliocene", "Miocene", "Oligocene", "Eocene", "Paleocene". What code did you use? Which two epochs are the most dissimilar?

> vegdist(PresencePBDB[c(15,19,20,21,27,23),1:903], method="jaccard", binary=FALSE, na.rm=FALSE)
                Eocene  Paleocene  Oligocene    Miocene   Pliocene
Paleocene   0.33385827                                            
Oligocene   0.19063005 0.41042345                                 
Miocene     0.08585056 0.33333333 0.16065574                      
Pliocene    0.13397129 0.37914692 0.18968386 0.08496732           
Pleistocene 0.21870048 0.44444444 0.26910299 0.17207792 0.12692967

#Paleocene and Pleistocene are the most dissimilar with a Jaccard distance of 0.44444444

## Problem Set III

1) Create a subset of the PresencePBDB matrix which contains just the following rows - "Pliocene", "Oligocene", "Paleocene", "Early Cretaceous", "Late Jurassic", and "Middle Jurassic". Name this subset RandomEpochs. Show your code.

> RandomEpochs<-PresencePBDB[c(27,20,19,17,14,18), ]

2) Using vegdist( ) find the dissimilarities of all the epochs in Random Epochs. Show your code.

> vegdist(RandomEpochs[ , ], method="jaccard", binary=FALSE, na.rm=FALSE)
                  Pliocene Oligocene Paleocene Early Cretaceous Late Jurassic
Oligocene        0.1896839                                                   
Paleocene        0.3791469 0.4104235                                         
Early Cretaceous 0.7462908 0.7480315 0.6400742                               
Late Jurassic    0.8652695 0.8653846 0.7902622        0.4703947              
Middle Jurassic  0.8852459 0.8814103 0.7931689        0.4883721     0.2962963

3) Find the two epochs that are the most dissimilar and make them the poles. Now, using the dissimilarities, order (ordinate) the remaining epochs based on their similarity to the poles. State the order of your inferred gradient.

#Pliocene and Middle Jurassic are most dissimilar with a Jaccard distance of 0.8852459
#Order of inferred gradient: Pliocene, Oligocene, Paleocene, Early Cretaceous, Late Jurassic, Middle Jurassic

4) Can you deduce what "variable" is controlling this gradient (e.g., temperature, water depth, geographic distance)? [Hint: Check the geologic timescale]. State your reasoning.

#variable controlling gradient is the geological time distance. The poles are the earliest and the latest epochs (having the farthest temporal distance from each other), with the other epochs arranged in temporal order between the two poles.

5). There is a relatively high dissimilarity between the Early Cretaceous and Paleocene epochs. Can you hypothesize why this is? Google these epochs if you need to.
There is a high dissimilarity between the Early Cretaceous and Paleocene epochs (or at the K-T boundary) because it is also the boundary of mass extinction where many species went extinct. There was a large change in global enviromental conditions including temperature and climate that would have changed the niches and open up opportunities for new species to thrive.

-----------------------------------------------------------------------
Problem Set IV

1) Download a dataset from the paleobiology database of all Ordovician aged animals (i.e., animalia) into R, and name the object Ordovician. This may take a few minutes. What R code did you use?

OrdovicianOriginal<-downloadPBDB(Taxa=c("animalia"),StartInterval="Ordovician",StopInterval="Ordovician")

2) Clean up the poorly resolved genus names. What function/code did you use?

Ordovician<-cleanGenus(Ordovician)

3) Turn your object Ordovician into a community matrix of samples by genera, where the samples are different geoplate codes. Geoplate codes denote different ancient paleocontinents - i.e., your community matrix will list which genera were present in which ancient paleocontinent. Cull this matrix so that each sample has a minimum of 25 taxa and each taxon occurs in at least two samples. Show your code.

Ordovician<-presenceMatrix(Ordovician,SampleDefinition="geoplate")
Ordovician<-cullMatrix(Ordovician,minOccurrences=2,minDiversity=25)

4) Perform a DCA on your new community matrix. Analyze your new DCA with a plot. Do you think that the orientation of samples along either axis 1 or axis 2 is related to the average latitude or longitude of each plate in question? Explain how you figured this out. Show your code. [Hint: Information about the paleolatitude and paleolongitude of different geoplates is included in your originally downloaded data - i.e., the object Ordovician.]

> OrdovicianDCA<-decorana(Ordovician,ira=0)
> plot(OrdovicianDCA,display="sites")

> tapply(OrdovicianOriginal[ ,"paleolat"],OrdovicianOriginal[ ,"geoplate"], mean)
         0        101        102        103        104        106        108        109        123        127        128        129        130        201        291 
 40.503824 -10.224898  10.316633  28.190000  11.830938  12.729819 -43.661739 -74.469000  21.465473   5.582324  31.391562  -0.550000  18.600930 -32.661837 -28.016373 
       302        303        304        305        307        309        311        313        315        401        402        405        407        501        503 
-26.998844   3.125000 -79.274050 -69.228498 -60.243750  12.970000  21.206293 -10.745430 -43.644852  12.063369 -14.182127  15.940000  -4.043939 -23.376087 -52.998462 
       505        512        601        602        604        611        612        616        628        701        707        714        715        800        801 
-49.004812 -49.104571 -10.122569  34.157864  27.050609 -10.314543 -14.100000  11.488571  24.981222 -36.650000 -75.460000 -81.510599 -69.800000  24.330000   8.788138 
       802        806 
  0.230000   8.709483 

> tapply(OrdovicianOriginal[ ,"paleolng"],OrdovicianOriginal[ ,"geoplate"], mean)
          0         101         102         103         104         106         108         109         123         127         128         129         130         201         291 
 -30.750000 -111.026331  -69.256939  -92.998033 -132.038000  -84.745361  -89.086957 -118.558000 -117.624328 -125.453760 -128.791250 -131.580000 -126.702791 -149.269458  -38.752803 
        302         303         304         305         307         309         311         313         315         401         402         405         407         501         503 
 -63.430133  -72.830000  -12.037017    4.842639   31.301250  -67.650000  -62.632293  -82.207983  -82.437376  -42.074589   30.883153  -84.820000   30.247879   89.080326   88.780000 
        505         512         601         602         604         611         612         616         628         701         707         714         715         800         801 
  80.031955   64.780000   62.746111  111.283495   94.010378   80.764724   96.800000   82.130306   -7.847778  143.740000  -97.920000  -66.896028   46.420000  100.200000  118.506900 
        802         806 
 137.840000  135.354335 

  #the geoplates plotted at more positive DCA1 values are farther towards the Southern hemisphere whereas geoplates plotted at towards more negative DCA1 values are farther northwards (e.g. geoplate 714 is at -81 latitude, geoplate 102 is at 10 latitude)
  
  > Interesting, many people did not report a relationship.
