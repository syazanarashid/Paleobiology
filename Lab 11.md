Tuan Syazana Tuan Ab Rashid
Lab 11 - due April 25,2016

> 18.5/20

## PART 1

## Problem Set 1

1) You first mission is to download a list of all Triassic units in the Macrostrat Database using the /units route into R. Name this object TriassicUnits. As always, show your code.
````R
> URL<-"https://macrostrat.org/api/units?interval_name=Triassic&format=csv"
> TriassicUnits<-read.csv(URL,row.names=1)
````

2) How many Triassic units did you download? What code did you use to find out?
````R
> nrow(TriassicUnits)
[1] 838
````
3) Look at the first 10 units that you downloaded. Are they mostly Igenous, Metamorphic, or Sedimentary rocks? Do you believe that these units are relevant for an investigation of fossil preservation? Show your code and explain your reasoning.
````R
> TriassicUnits[1:10,]
````
They are mostly igneous and metamorphic rocks. I don't think they are relevant for an investigation of fossil preservation because they would very likely be destroyed under the high pressures and temperatures.

4) Which columns of your TriassicUnits data.frame denote the starting age and ending age of each unit, respectively?

The "t_age" denote the ending age and the "b_age" denote the starting age.

5) Considering the bottom and top ages of the first 10 units, are these units constrained to only the Triassic or do some range through the Triassic?

They range through the Triassic.

## Problem Set 2

1) Re-download TriassicUnits, however, this time restrict the data to only sedimentary rocks. Show your code.

Hints:

/units documentation may provide some hepful information.
/defs/lithologies may provide some helpful information.
As before, use the read.csv( ) function and set the output format to csv.

2) Restrict TriassicUnits to only units that with starting ages <= start of the Triassic and ending ages >= to the end of the Triassic. As always, show your code.

````R
> URLSedTriassicUnits<-"https://macrostrat.org/api/units?interval_name=Triassic&lith_class=sedimentary&format=csv"
> SedTriassicUnits<-read.csv(URLSedTriassicUnits,row.names=1)
````

Hints:

You will want to use either the which( ) or subset( ) functions.
You will have to make use of logical operators >=, <=, and &. For a review of these, see the logical operators and subsetting with logical operators sections of the R Tutorial.

3) Repeat the above processes (download and subset) for the following geologic periods. The Cretaceous, Jurassic, Triassic (you don't have to download it twice), Permian, Carboniferous, Devonian, Silurian, and Ordovician. Show your code, but do not show me the downloaded data.
````R
> URLSedCretaceousUnits<-"https://macrostrat.org/api/units?interval_name=Cretaceous&lith_class=sedimentary&format=csv"
> SedCretaceousUnits<-read.csv(URLSedCretaceousUnits,row.names=1)

> URLSedJurassicUnits<-"https://macrostrat.org/api/units?interval_name=Jurassic&lith_class=sedimentary&format=csv"
> SedJurassicUnits<-read.csv(URLSedJurassicUnits,row.names=1)

> URLSedTriassicUnits<-"https://macrostrat.org/api/units?interval_name=Triassic&lith_class=sedimentary&format=csv"
> SedTriassicUnits<-read.csv(URLSedTriassicUnits,row.names=1)

> URLSedPermianUnits<-"https://macrostrat.org/api/units?interval_name=Permian&lith_class=sedimentary&format=csv"
> SedPermianUnits<-read.csv(URLSedPermianUnits,row.names=1)

> URLSedCarboniferousUnits<-"https://macrostrat.org/api/units?interval_name=Carboniferous&lith_class=sedimentary&format=csv"
> SedCarboniferousUnits<-read.csv(URLSedCarboniferousUnits,row.names=1)

> URLSedDevonianUnits<-"https://macrostrat.org/api/units?interval_name=Devonian&lith_class=sedimentary&format=csv"
> SedDevonianUnits<-read.csv(URLSedDevonianUnits,row.names=1)

> URLSedSilurianUnits<-"https://macrostrat.org/api/units?interval_name=Silurian&lith_class=sedimentary&format=csv"
> SedSilurianUnits<-read.csv(URLSedSilurianUnits,row.names=1)

> URLSedOrdovicianUnits<-"https://macrostrat.org/api/units?interval_name=Ordovician&lith_class=sedimentary&format=csv"
> SedOrdovicianUnits<-read.csv(URLSedOrdovicianUnits,row.names=1)
````

4) Make a vector named UnitFreqs that records the number of units present in each epoch. Show your code.

````R
UnitFreqs<-c(nrow(SedCretaceousUnits),nrow(SedJurassicUnits),nrow(SedTriassicUnits),nrow(SedPermianUnits),nrow(SedCarboniferousUnits),nrow(SedDevonianUnits),nrow(SedSilurianUnits),nrow(SedOrdovicianUnits))
> UnitFreqs
[1] 4929 1234  713 1081 3331 2399 1493 2512
````

5) Find the mean and standard deviation of UnitFreqs not counting the Triassic. How many standard deviations above or below the mean is the number of Triassic Units? Show your code.

````R
#UnitFreqs minus element 3
> NewUnitFreqs<-UnitFreqs[-3]
> NewUnitFreqs
[1] 4929 1234 1081 3331 2399 1493 2512

> mean(NewUnitFreqs)
[1] 2425.571
> sd(NewUnitFreqs)
[1] 1365.805

> (2425.571-713)/1365.805
[1] 1.253891
#the number of Triassic Units is 1.253891 standard deviations below the mean.
````

6) Given your answer to the above, do you believe that the Triassic has a statistically lower number of units than the other periods? Why?

Yes, because it is 1.253891 standard deviations below the mean.

> That's not an explanation! -1 Points

7) What if you consider both the Triassic and Jurassic as potential outliers? Explain (show your code) how you arrived at your answer.

````R
> NewestUnitFreqs
[1] 4929  713 1081 3331 2399 1493 2512
> mean(NewestUnitFreqs)
[1] 2351.143
> sd(NewestUnitFreqs)
[1] 1452.975 

> (2351.143-713)/1452.975
[1] 1.127441
````

> -0.5 points

## PART 2

## Problem Set 3

1) Download and plot a map of all North American geologic columns (no color). Show your code.

````R
>URLall<-"https://macrostrat.org/api/columns?format=geojson_bare&project_id=1"
>URLall<-getURL(URLall)
>NorthAmerica<-readOGR(URLall,"OGRGeoJSON",verbose=FALSE)
>plot(NorthAmerica,col=)
````

2) On top of your map from Question 1, plot a map of all North American columns with Induan-Anisian sedimentary units. Use the Olenekian hexcode color for this map. You can look up the Olenekian hexcode through the /defs/intervals route.

````R
#North America with Induan-Anisian units
>URLallIA<-"https://macrostrat.org/api/columns?format=geojson_bare&age_top=242&age_bottom=252&project_id=1"
>URLallIA<-getURL(URLallIA)
>IA<-readOGR(URLallIA,"OGRGeoJSON",verbose=FALSE)
>plot(IA,col="#B051A5",add=TRUE)
````

3) Using the downloadPBDB( ) function from previous labs. Download all occurrences of animal fossils in the Paleobioslogy Database of Induan-Anisian age. Using the points( ) function, plot all of these occurrences on the map you made in question 2 as solid circles. If you do not remember how to use points, you can consult previous labs or use help(points). Show your code. Save this map for later questions.

````R
>IA<-downloadPBDB(Taxa=c("Animalia"),StartInterval="Induan",StopInterval="Anisian")
>points(IA[ ,"lng"],IA[ ,"lat"],pch=20,col="lightgreen")
````

4) You can open a new plot window using quartz( ) if you are on a mac or `windows( ) if you are on a windows machine. Download and plot a map of all North American geologic columns (no color) - i.e., repeat Question 1 in this new plot window. On top of this map, plot a map of all North American columns with Lopingian aged sedimentary units. Use the appropriate Lopingian hexcode color for this new map. Show your code.

````R
#North America
>URLall<-"https://macrostrat.org/api/columns?format=geojson_bare&project_id=1"
>URLall<-getURL(URLall)
>NorthAmerica<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
>plot(NorthAmerica,col=)

#Lopingian Units
>URL<-"https://macrostrat.org/api/columns?format=geojson_bare&age_top=252&age_bottom=260&project_id=1"
>URLallLop<-getURL(URLallLop)
>Lop<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
>plot(Lop,col="#FBA794",add=TRUE)
````

5) Download all occurrences of animal fossils in the Paleobiology Database of Lopingian age. Plot all of these occurrences on the map you made in question 2 as solid circles. Show your code.

````R
#North America map with Lopingian units
>URLall<-"https://macrostrat.org/api/columns?format=geojson_bare&age_top=252&age_bottom=260&project_id=1"
>URLall<-getURL(URLall)
>Lop<-readOGR(GotURL,"OGRGeoJSON",verbose=FALSE)
>plot(Lop,col="#FBA794",add=TRUE)

#Download Lopingian fossils and plotting points
>LopFossil<-downloadPBDB(Taxa=c("Animalia"),StartInterval="Lopingian",StopInterval="Lopingian")
>points(LopFossil[ ,"lng"],LopFossil[ ,"lat"],pch=20,col="blue")
````

6) Compare and contrast your Induan-Anisian map versus your Lopingian map. Does it seem based on these maps that...

a) There was a substantial drop in the areal extent of North American sedimentary units across the P/T boundary.

Yes. There are more sedimentary units for the Permian than the Triassic hence, a probable rise in sea-level indicating a drop in aerial extent.

b) There was a substantial drop in the percentage of sedimentary units with reported fossils in them aross the P/T boundary?

No. It seems like there is an increase in the percentage of sedimentary units with reported fossils in them aross the P/T boundary.

c) Overall, do you think there is sufficient evidence from these maps to reject or accept the hypothesis that lower diversity in the Early Triassic is an artefact of either poor fossil sampling of the available sedimentary rock or a low availablility of sedimentary rock.

I do not think there is sufficient evidence to asses diversity in the Early Triassic since our maps pull data on occurances rather than diversity. In addition, we did not use any diversity metrics to compare and contrast over the P/T boundary. Also, it seems that we can reject the hypothesis of low availablility of sedimentary rock since there were lower fossil data occurence with the higher availablility of sedimentary rock in the Permian. 
