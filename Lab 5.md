Tuan Syazana Tuan Ab Rashid
Lab 5 - due Feb 22,2016

> 18/20

## Problem Set 1

1) What is Bivalve generic richness in the Miocene? What code did you use to find out?

````R
> BivalveRichness<-which((BivalveAbundance["Miocene", ]) !=0)
> length(BivalveRichness)
[1] 634
````

2) What is the Berger-Parker Index of Brachiopods genera in the Pliocene? What code did you use to find out? [Hint: the function max( ) may help you).

````R
> BrachiopodPliocenemax<-max(BrachiopodAbundance["Pliocene", ])
> BrachiopodPliocenesum<-sum(BrachiopodAbundance["Pliocene", ])
> BrachiopodPliocenemax/BrachiopodPliocenesum
[1] 0.2222222
````

3) What is the Gini-Simpson Index of Brachiopods during the Late Ordovician? What code did you use to find out?

````R
> BrachiopodLateOrdoviciansum<-sum(BrachiopodAbundance["Late Ordovician", ])
> BrachiopodLateOrdoviciansum
[1] 6154
> AbundancesBLO<-BrachiopodAbundance["Late Ordovician", ] 
> 1 - sum((AbundancesBLO/BrachiopodLateOrdoviciansum)^2) 
[1] 0.9784588
````

4) What is the Shannon's Entropy of Bivalves during the Late Cretaceous? What code did you use to find out?

````R
> BivalveLCsum<-sum(BivalveAbundance["Late Cretaceous", ])
> AbundanceBLC<-BivalveAbundance["Late Cretaceous", ]
> NewAbundanceBLC<-AbundanceBLC[AbundanceBLC>0]
> A <-NewAbundanceBLC/BivalveLCsum
> B <-log(NewAbundanceBLC/BivalveLCsum)
> C <-sum(A*B)
> -1*C
[1] 5.086654
````

5) What is the Shannon's Entropy of Bivalves during the Paleocene? What code did you use to find out?

````R
> BivalvePsum<-sum(BivalveAbundance["Paleocene", ])
> AbundanceBP<-BivalveAbundance["Paleocene", ]
> NewAbundanceBP<-AbundanceBP[AbundanceBP>0]
> A <-NewAbundanceBP/BivalvePsum
> B <-log(NewAbundanceBP/BivalvePsum)
> C <-sum(A*B)
> -1*C
[1] 4.511063
````

6) What is the percent change in Shannon's Entropy between the Late Cretaceous and the Paleocene? Can you think of any major events that happened between the Late Cretaceous and Paleocene that might be relevant to biodiversity? [Hint: Use google if you don't know.] Is this reflected in this index?

````R
> ((4.511063 - 5.086654)/5.086654)*100 
[1] -11.31571
`````

The percent change in Shannon’s Entropy between the Late Cretaceous and the Palaeocene is -11.31571%. The K/Pg mass extinction event. Yes this is reflected by the negative percent change of the index.

7) What if you use the exp( ) function to exponentiate the Shannon's Entropies you calculated in questions 4,5, and 6 (i.e., e^Shannon's Entropy)? What percent of diversity is gained/lost? Does this better reflect the change between the Late Cretaceous and Paleocene? Why or why not?

````R
e^(Shannon's Entropy of Bivalves during the Late Cretaceous)
> exp(5.086654)
[1] 161.8474

e^(Shannon's Entropy of Bivalves during the Paleocene)
> exp(4.511063)
[1] 91.01852

> ((91.01852 - 161.8474)/161.8474)*100
[1] -43.76275
`````

The percent change in Shannon’s Entropy between the Late Cretaceous and the Palaeocene is -43.76275% 

I think it better reflects the change between the Late Cretaceous and Paleocene because it provides a bigger range of values.

## Problem Set 2

Install (if you have not already) and load the vegan package into R. Read the help file for the diversity( ) function - ?diversity or help(diversity). You must have already loaded the vegan package in order for it to run.

1) Use the specnumber( ) function (also from the vegan package) to find Bivalve richness in the Miocene. What code did you use to find out?

````R
> specnumber(BivalveAbundance["Miocene", ], , MARGIN = 1)
[1] 634
````

2) Use the diversity( ) function to find the Gini-Simpson Index of Brachiopods during the Late Ordovician? What code did you use to find out?

````R
> diversity(BrachiopodAbundance["Late Ordovician", ], index = "simpson", MARGIN = 1, base = exp(1))
[1] 0.9784588
````

3) Use the diversity( ) function to find the Shannon's Entropy of Bivalves during the Late Cretaceous? What code did you use to find out?

````R
> diversity(BivalveAbundance["Late Cretaceous", ], index = "shannon", MARGIN = 1, base = exp(1))
[1] 5.086512
````

4) Use the diversity( ) function to find the Shannon's Entropy of Bivalves during the Paleocene? What code did you use to find out?

````R
> diversity(BivalveAbundance["Paleocene", ], index = "shannon", MARGIN = 1, base = exp(1))
[1] 4.511063
````

## Problem Set 3

````R
> specnumber(BivalveAbundance, )
    Pennsylvanian Middle Ordovician   Late Ordovician        Llandovery           Wenlock            Ludlow 
              104                48                87                56                66                81 
          Pridoli     Mississippian    Early Devonian   Middle Devonian     Late Devonian        Cisuralian 
               51                99               111                88                70               160 
    Late Jurassic            Eocene   Late Cretaceous  Early Cretaceous   Middle Jurassic  Early Ordovician 
              270               512               573               393               202                42 
        Paleocene           Miocene         Oligocene    Early Jurassic       Pleistocene       Guadalupian 
              304               634               355               217               498               191 
  Middle Triassic     Late Triassic          Pliocene         Lopingian    Early Triassic 
              151               242               534               156               101 
> specnumber(BrachiopodAbundance, )
    Mississippian     Pennsylvanian  Early Ordovician Middle Ordovician   Late Ordovician        Llandovery 
              314               284               141               282               331               271 
          Wenlock            Ludlow           Pridoli    Early Devonian   Middle Devonian     Late Devonian 
              257               234               138               497               353               274 
       Cisuralian     Late Jurassic            Eocene   Late Cretaceous  Early Cretaceous   Middle Jurassic 
              564               111                57                96               125               175 
        Paleocene         Lopingian    Early Jurassic       Guadalupian   Middle Triassic     Late Triassic 
               29               406               130               549               111               193 
          Miocene    Early Triassic          Pliocene       Pleistocene         Oligocene 
               45                63                23                19                30 
> OutOrderRichBivalve<-array(c(104, 48, 87, 56, 66, 81, 51, 99, 111, 88, 70, 160, 270, 512, 573, 393, 202, 42, 304, 634, 355, 217, 498, 191, 151, 242, 534, 156, 101),dimnames=list(c("Pennsylvanian", "Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli", "Mississippian", "Early Devonian", "Middle Devonian", "Late Devonian", "Cisuralian", "Late Jurassic", "Eocene", "Late Cretaceous", "Early Cretaceous", "Middle Jurassic", "Early Ordovician", "Paleocene", "Miocene", "Oligocene", "Early Jurassic", "Pleistocene", "Guadalupian", "Middle Triassic",  "Late Triassic", "Pliocene", "Lopingian", "Early Triassic")))
> OutOrderRichBivalve
    Pennsylvanian Middle Ordovician   Late Ordovician        Llandovery           Wenlock            Ludlow 
              104                48                87                56                66                81 
          Pridoli     Mississippian    Early Devonian   Middle Devonian     Late Devonian        Cisuralian 
               51                99               111                88                70               160 
    Late Jurassic            Eocene   Late Cretaceous  Early Cretaceous   Middle Jurassic  Early Ordovician 
              270               512               573               393               202                42 
        Paleocene           Miocene         Oligocene    Early Jurassic       Pleistocene       Guadalupian 
              304               634               355               217               498               191 
  Middle Triassic     Late Triassic          Pliocene         Lopingian    Early Triassic 
              151               242               534               156               101 
> InOrderRichBivalve<-OutOrderRichBivalve[c("Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli","Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian", "Cisuralian", "Guadalupian", "Lopingian", "Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous", "Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene")]
> InOrderRichBivalve
Middle Ordovician   Late Ordovician        Llandovery           Wenlock            Ludlow           Pridoli 
               48                87                56                66                81                51 
   Early Devonian   Middle Devonian     Late Devonian     Mississippian     Pennsylvanian        Cisuralian 
              111                88                70                99               104               160 
      Guadalupian         Lopingian    Early Triassic   Middle Triassic     Late Triassic    Early Jurassic 
              191               156               101               151               242               217 
  Middle Jurassic     Late Jurassic  Early Cretaceous   Late Cretaceous         Paleocene            Eocene 
              202               270               393               573               304               512 
        Oligocene           Miocene          Pliocene       Pleistocene 
              355               634               534               498 
> OutOrderRichBrachiopod<-array(c(314, 284, 141, 282, 331, 271, 257, 234, 138, 497, 353, 274, 564, 111, 57, 96, 125, 175, 29, 406, 130, 549, 111, 193, 45, 63, 23, 19, 30),dimnames=list(c("Mississippian", "Pennsylvanian", "Early Ordovician", "Middle Ordovician", "Late Ordovician", "Llandovery", "Wenlock", "Ludlow", "Pridoli", "Early Devonian", "Middle Devonian", "Late Devonian", "Cisuralian", "Late Jurassic", "Eocene", "Late Cretaceous", "Early Cretaceous", "Middle Jurassic", "Paleocene", "Lopingian", "Early Jurassic", "Guadalupian", "Middle Triassic", "Late Triassic", "Miocene", "Early Triassic", "Pliocene", "Pleistocene", "Oligocene")))
> 
> OutOrderRichBrachiopod
    Mississippian     Pennsylvanian  Early Ordovician Middle Ordovician   Late Ordovician        Llandovery 
              314               284               141               282               331               271 
          Wenlock            Ludlow           Pridoli    Early Devonian   Middle Devonian     Late Devonian 
              257               234               138               497               353               274 
       Cisuralian     Late Jurassic            Eocene   Late Cretaceous  Early Cretaceous   Middle Jurassic 
              564               111                57                96               125               175 
        Paleocene         Lopingian    Early Jurassic       Guadalupian   Middle Triassic     Late Triassic 
               29               406               130               549               111               193 
          Miocene    Early Triassic          Pliocene       Pleistocene         Oligocene 
               45                63                23                19                30 
> InOrderRichBrachiopod<-OutOrderRichBrachiopod[c("Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli","Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian", "Cisuralian", "Guadalupian", "Lopingian", "Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous", "Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene")]
> 
> InOrderRichBrachiopod
Middle Ordovician   Late Ordovician        Llandovery           Wenlock            Ludlow           Pridoli 
              282               331               271               257               234               138 
   Early Devonian   Middle Devonian     Late Devonian     Mississippian     Pennsylvanian        Cisuralian 
              497               353               274               314               284               564 
      Guadalupian         Lopingian    Early Triassic   Middle Triassic     Late Triassic    Early Jurassic 
              549               406                63               111               193               130 
  Middle Jurassic     Late Jurassic  Early Cretaceous   Late Cretaceous         Paleocene            Eocene 
              175               111               125                96                29                57 
        Oligocene           Miocene          Pliocene       Pleistocene 
               30                45                23                19 
               
> diversity(BivalveAbundance, )
    Pennsylvanian Middle Ordovician   Late Ordovician        Llandovery 
         3.755572          3.227148          3.560792          3.148909 
          Wenlock            Ludlow           Pridoli     Mississippian 
         3.628257          3.567614          3.294253          3.844638 
   Early Devonian   Middle Devonian     Late Devonian        Cisuralian 
         3.988784          3.397504          3.149485          4.259922 
    Late Jurassic            Eocene   Late Cretaceous  Early Cretaceous 
         4.571792          4.922718          5.086512          4.894056 
  Middle Jurassic  Early Ordovician         Paleocene           Miocene 
         4.410415          3.357938          4.511063          5.375537 
        Oligocene    Early Jurassic       Pleistocene       Guadalupian 
         4.972140          4.299667          5.267982          4.454766 
  Middle Triassic     Late Triassic          Pliocene         Lopingian 
         4.127591          4.516975          5.334865          4.160419 
   Early Triassic 
         2.905877 
> diversity(BrachiopodAbundance, )
    Mississippian     Pennsylvanian  Early Ordovician Middle Ordovician 
         4.618776          4.096848          4.200277          4.859976 
  Late Ordovician        Llandovery           Wenlock            Ludlow 
         4.664635          4.535380          4.658886          4.664010 
          Pridoli    Early Devonian   Middle Devonian     Late Devonian 
         4.325749          5.296419          4.546489          4.398376 
       Cisuralian     Late Jurassic            Eocene   Late Cretaceous 
         5.353992          3.927540          3.338419          3.517404 
 Early Cretaceous   Middle Jurassic         Paleocene         Lopingian 
         4.085487          4.164713          2.500670          4.734245 
   Early Jurassic       Guadalupian   Middle Triassic     Late Triassic 
         3.729191          5.325329          3.824816          4.185167 
          Miocene    Early Triassic          Pliocene       Pleistocene 
         3.216753          3.125604          2.611886          2.573816 
        Oligocene 
         3.106048 
> 
> OutOrderBivalve<-array(c(3.755572,3.227148,3.560792,3.148909,3.628257,3.567614,3.294253,3.844638, 3.988784, 3.397504, 3.149485, 4.259922, 4.571792, 4.922718, 5.086512, 4.894056, 4.410415, 3.357938, 4.511063, 5.375537, 4.972140, 4.299667, 5.267982, 4.454766, 4.127591, 4.516975, 5.334865, 4.160419, 2.905877),dimnames=list(c("Pennsylvanian", "Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli", "Mississippian", "Early Devonian", "Middle Devonian", "Late Devonian", "Cisuralian", "Late Jurassic", "Eocene", "Late Cretaceous", "Early Cretaceous", "Middle Jurassic", "Early Ordovician", "Paleocene", "Miocene", "Oligocene", "Early Jurassic", "Pleistocene", "Guadalupian", "Middle Triassic",  "Late Triassic", "Pliocene", "Lopingian", "Early Triassic")))
> OutOrderBivalve
    Pennsylvanian Middle Ordovician   Late Ordovician        Llandovery           Wenlock 
         3.755572          3.227148          3.560792          3.148909          3.628257 
           Ludlow           Pridoli     Mississippian    Early Devonian   Middle Devonian 
         3.567614          3.294253          3.844638          3.988784          3.397504 
    Late Devonian        Cisuralian     Late Jurassic            Eocene   Late Cretaceous 
         3.149485          4.259922          4.571792          4.922718          5.086512 
 Early Cretaceous   Middle Jurassic  Early Ordovician         Paleocene           Miocene 
         4.894056          4.410415          3.357938          4.511063          5.375537 
        Oligocene    Early Jurassic       Pleistocene       Guadalupian   Middle Triassic 
         4.972140          4.299667          5.267982          4.454766          4.127591 
    Late Triassic          Pliocene         Lopingian    Early Triassic 
         4.516975          5.334865          4.160419          2.905877 
> InOrderBivalve<-OutOrderBivalve[c("Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli","Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian", "Cisuralian", "Guadalupian", "Lopingian", "Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous", "Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene")]
> InOrderBivalve
Middle Ordovician   Late Ordovician        Llandovery           Wenlock            Ludlow 
         3.227148          3.560792          3.148909          3.628257          3.567614 
          Pridoli    Early Devonian   Middle Devonian     Late Devonian     Mississippian 
         3.294253          3.988784          3.397504          3.149485          3.844638 
    Pennsylvanian        Cisuralian       Guadalupian         Lopingian    Early Triassic 
         3.755572          4.259922          4.454766          4.160419          2.905877 
  Middle Triassic     Late Triassic    Early Jurassic   Middle Jurassic     Late Jurassic 
         4.127591          4.516975          4.299667          4.410415          4.571792 
 Early Cretaceous   Late Cretaceous         Paleocene            Eocene         Oligocene 
         4.894056          5.086512          4.511063          4.922718          4.972140 
          Miocene          Pliocene       Pleistocene 
         5.375537          5.334865          5.267982 
> 
> OutOrderBrachiopod<-array(c(4.618776, 4.096848, 4.200277, 4.859976, 4.664635, 4.535380, 4.658886, 4.664010, 4.325749, 5.296419, 4.546489, 4.398376, 5.353992, 3.927540, 3.338419, 3.517404, 4.085487, 4.164713, 2.500670, 4.734245, 3.729191, 5.325329, 3.824816, 4.185167, 3.216753, 3.125604, 2.611886, 2.573816, 3.106048),dimnames=list(c("Mississippian", "Pennsylvanian", "Early Ordovician", "Middle Ordovician", "Late Ordovician", "Llandovery", "Wenlock", "Ludlow", "Pridoli", "Early Devonian", "Middle Devonian", "Late Devonian", "Cisuralian", "Late Jurassic", "Eocene", "Late Cretaceous", "Early Cretaceous", "Middle Jurassic", "Paleocene", "Lopingian", "Early Jurassic", "Guadalupian", "Middle Triassic", "Late Triassic", "Miocene", "Early Triassic", "Pliocene", "Pleistocene", "Oligocene")))
> OutOrderBrachiopod
    Mississippian     Pennsylvanian  Early Ordovician Middle Ordovician   Late Ordovician 
         4.618776          4.096848          4.200277          4.859976          4.664635 
       Llandovery           Wenlock            Ludlow           Pridoli    Early Devonian 
         4.535380          4.658886          4.664010          4.325749          5.296419 
  Middle Devonian     Late Devonian        Cisuralian     Late Jurassic            Eocene 
         4.546489          4.398376          5.353992          3.927540          3.338419 
  Late Cretaceous  Early Cretaceous   Middle Jurassic         Paleocene         Lopingian 
         3.517404          4.085487          4.164713          2.500670          4.734245 
   Early Jurassic       Guadalupian   Middle Triassic     Late Triassic           Miocene 
         3.729191          5.325329          3.824816          4.185167          3.216753 
   Early Triassic          Pliocene       Pleistocene         Oligocene 
         3.125604          2.611886          2.573816          3.106048 
> InOrderBrachiopod<-OutOrderBrachiopod[c("Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli","Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian", "Cisuralian", "Guadalupian", "Lopingian", "Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous", "Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene")]
> InOrderBrachiopod
Middle Ordovician   Late Ordovician        Llandovery           Wenlock            Ludlow 
         4.859976          4.664635          4.535380          4.658886          4.664010 
          Pridoli    Early Devonian   Middle Devonian     Late Devonian     Mississippian 
         4.325749          5.296419          4.546489          4.398376          4.618776 
    Pennsylvanian        Cisuralian       Guadalupian         Lopingian    Early Triassic 
         4.096848          5.353992          5.325329          4.734245          3.125604 
  Middle Triassic     Late Triassic    Early Jurassic   Middle Jurassic     Late Jurassic 
         3.824816          4.185167          3.729191          4.164713          3.927540 
 Early Cretaceous   Late Cretaceous         Paleocene            Eocene         Oligocene 
         4.085487          3.517404          2.500670          3.338419          3.106048 
          Miocene          Pliocene       Pleistocene 
         3.216753          2.611886          2.573816 
````

> You don't need to show the tables next time, just the code you write.

1) Is brachiopod richness positively, negatively, or un-correlated with bivalve richness? Show your code?

````R
> VectorRichBivalve<-c(48, 87, 56, 66, 81, 51, 111, 88, 70, 99, 104, 160, 191, 156, 101, 151, 242, 217, 202, 270, 393, 573, 304, 512, 355, 634, 534, 498)
> VectorRichBrachiopod<-c(282, 331, 271, 257, 234, 138, 497, 353, 274, 314, 284, 564, 549, 406, 63, 111, 193, 130, 175, 111, 125, 96, 29, 57, 30, 45, 23, 19)
> cor(VectorRichBivalve,VectorRichBrachiopod)
[1] -0.596469
> #Brachiopod richness is negatively correlated with bivalve richness.
````

2) Is brachiopod biodiversity positively, negatively, or un-correlated with bivalve biodiversity when using the Gini-Simpson index? Show your code?

````R
> VectorBivalve<-c(3.227148, 3.560792, 3.148909, 3.628257, 3.567614, 3.294253, 3.988784, 3.397504, 3.149485, 3.844638, 3.755572, 4.259922, 4.454766, 4.160419, 2.905877, 4.127591, 4.516975, 4.299667, 4.410415, 4.571792, 4.894056, 5.086512, 4.511063, 4.922718, 4.972140, 5.375537, 5.334865, 5.267982)
> VectorBrachiopod<-c(4.859976, 4.664635, 4.535380, 4.658886, 4.664010, 4.325749, 5.296419, 4.546489, 4.398376, 4.618776, 4.096848, 5.353992, 5.325329, 4.734245, 3.125604, 3.824816, 4.185167, 3.729191, 4.164713, 3.927540, 4.085487, 3.517404, 2.500670, 3.338419, 3.106048, 3.216753, 2.611886, 2.573816)
> cor(VectorBivalve,VectorBrachiopod)
[1] -0.5362931

#Brachiopod biodiversity is negatively correlated with bivalve biodiversity.
````

3) Looking just at changes in brachiopod richness through time, when did the greatest drop in brachiopod richness occur (i.e., between what two consecutive epochs)?

Between the K/Pg boundary, that is, between the Late Cretaceous and the Palaeocene epochs.

> No, between the Lopingian and Early-Triassic. -1 Points

## Problem Set 4

1) Repeat the above steps, but for the BrachiopodAbundance community matrix. What is the standardized richness you got for brachiopods. Show your code.

````R
> SampleAbundancesBr<-apply(BrachiopodAbundance,1,sum)
> SampleAbundancesBr[which(SampleAbundancesBr==min(SampleAbundancesBr))]
Pleistocene 
         63 
> StandardizedRichnessBr<-apply(BrachiopodAbundance,1,subsampleIndividuals,Quota=63)
> StandardizedRichnessBr[1:6]
    Mississippian     Pennsylvanian  Early Ordovician Middle Ordovician   Late Ordovician        Llandovery 
            42.67             35.05             38.36             46.27             42.18             41.58 
````

2) How does the standardized brachiopod richness (previous question) compare to the unstandardized brachiopod richness from Problem Set 3? Show your code. Explain your reasoning. [Hint: Don't forget to put your biodiversities in temporal order]

````R
> OutOrderStandBr<-array(c(42.44, 34.27, 38.20, 46.17, 42.18, 41.34, 43.56, 44.49, 40.13, 50.02, 40.88, 39.25, 50.98, 33.86, 27.43, 28.95, 36.35, 37.18, 16.87, 43.14, 31.08, 50.61, 32.97, 37.05, 24.47, 23.95, 18.75, 19.00, 25.47),dimnames=list(c("Mississippian", "Pennsylvanian", "Early Ordovician", "Middle Ordovician", "Late Ordovician", "Llandovery", "Wenlock", "Ludlow", "Pridoli", "Early Devonian", "Middle Devonian", "Late Devonian", "Cisuralian", "Late Jurassic", "Eocene", "Late Cretaceous", "Early Cretaceous", "Middle Jurassic", "Paleocene", "Lopingian", "Early Jurassic", "Guadalupian", "Middle Triassic", "Late Triassic", "Miocene", "Early Triassic", "Pliocene", "Pleistocene", "Oligocene")))
> 
> InOrderStandBr<-OutOrderStandBr[c("Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli","Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian", "Cisuralian", "Guadalupian", "Lopingian", "Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous", "Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene")]
> VectorStandBr<-c(InOrderStandBr)
> VectorUnstandBr<-c(InOrderUnstandBr)
> cor(VectorStandBr,VectorUnstandBr)
[1] 0.9969244
> 
> # The standardized brachiopod richness is positively correlated to the unstandardized brachiopod richness. Both of them increase in value through time regardless if they have been standardized or not.
````

3) Make a scatter plot of standardized brachiopod richness versus standardized bivalve richness. Make a second scatter plot of unstandardized brachiopod richness versus unstandardized bivalve richness. Compare and contrast the two plots. What are the differences or similarities? Does standardizing or not standardizing matter? Show your code and explain your reasoning in detail. [Hint: If you forgot how to plot, revist the previous lab]

````R
> OutOrderStandBi<-array(c(43.54, 36.78, 41.99, 37.74, 46.34, 42.95, 34.67, 47.89, 51.21, 35.92, 33.26, 57.74, 64.50, 73.46, 78.77, 73.29, 61.67, 42.00, 63.66, 85.78, 76.90, 57.63, 84.14, 62.47, 54.00, 63.15, 85.68, 53.83, 27.61),dimnames=list(c("Pennsylvanian", "Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli", "Mississippian", "Early Devonian", "Middle Devonian", "Late Devonian", "Cisuralian", "Late Jurassic", "Eocene", "Late Cretaceous", "Early Cretaceous", "Middle Jurassic", "Early Ordovician", "Paleocene", "Miocene", "Oligocene", "Early Jurassic", "Pleistocene", "Guadalupian", "Middle Triassic",  "Late Triassic", "Pliocene", "Lopingian", "Early Triassic")))
> 
> InOrderStandBi<-OutOrderStandBi[c("Middle Ordovician","Late Ordovician","Llandovery","Wenlock","Ludlow","Pridoli","Early Devonian", "Middle Devonian", "Late Devonian", "Mississippian", "Pennsylvanian", "Cisuralian", "Guadalupian", "Lopingian", "Early Triassic", "Middle Triassic", "Late Triassic", "Early Jurassic", "Middle Jurassic", "Late Jurassic", "Early Cretaceous", "Late Cretaceous", "Paleocene", "Eocene", "Oligocene", "Miocene", "Pliocene", "Pleistocene")]
>
> plot(InOrderStandBr,InOrderStandBi)
> plot(InOrderRichBrachiopod,InOrderRichBivalve)
> #Both plots are negatively correlated but the standardized brachiopod richness versus standardized bivalve richness plot seems more linear whereas the unstandardized brachiopod richness versus unstandardized bivalve richness seems more exponential. The standardized richness standardized the data to the sample with the smallest abundance which resulted in a linear plot. The scale of the standardized richness plot is also smaller than the unstandardized richness plot.
````

4) Do you believe that there is any evidence in these analyses to support the idea that bivalves outcompeted brachiopods over time? Explain your reasoning.

Yes, since they are negatively correlated to each other. That is, the bivalve richness increased as the brachiopod richness decreased.

> A reasonable, but incomplete answer. -1 Points. Yes, they are negatiely correlated, but is that sufficient to prove the hypothesis?
