> 17.1/20

Tuan Syazana Tuan Ab Rashid
Paleobiology 
Lab 3 - Due Feb 15

## Question 1
1) How many collections are associated with this references?
704

2) What is the reference id number for the article?
24429

1) The first taxon in the taxonomic list is Rafinesquina alternata. Next to the taxonomic name is the citation (Conrad 1830), what is the significance of this citation?
 This is the first published description of that taxon.

2) What is the class, order, family, genus, and species name of the second taxon in the taxonomic list?
class: Strophomenata
order: Strophomenida
family: Strophomenidae
genus: Strophomena
species: planumbona

3) In what County was the data collected?
Union

4) What age (Period) is the data from?
Ordovician

5) What is the geologic formation where the data was found?
<strike>Richmondian Formation</strike> Lexington Limestone -1 Points

## Question 2
1) Zoom in so that you can see from Texas to Florida and from Florida to New York. You can zoom using the mouse wheel, by double-clicking, or clicking the + and - signs. Some of the occurrences are orange and others are yellow, what is the significance of the different colors?
The different colors correspond to the geologic time of the occurrences.

2) Zoom back out. Add an additional filter into the searchbar, the Ypresian stage. The Ypresian is a time interval ranging from 47.8–56.0 million years ago. In what countries are there Ypresian occurrences of Abra?
England, Belgium, USA

3) Clear the Abra and Ypresian filters from the search. Look for the genus Ambonychia. Within the United States find the city with the most occurrences of Ambonychia. What is the name of this city?
Cincinnati

4) What age (Period) are most Ambonychia occurrences?
Ordovician

1) During this time-period, were most occurrences of Ambonychia arrayed parallel or perpendicular to the equator?
parallel to the equator

2) Click on the little insect icon on the left side of the screen. This brings up taxonomic information on the target taxon. What order does Ambonychia belong to?
Myalinida

## Questions 3

1) What is the appropriate URL for downloading all occurrences of Ambonychia in the Lexington Limestone as a JSON?
https://training.paleobiodb.org/data1.2/occs/list.json?datainfo&rowcount&base_name=Ambonychia&strat=Lexington Limestone

2) What is the appropriate URL for downloading all occurrences of mammals present in the Paleocene through Oligocene epochs as a csv?
https://training.paleobiodb.org/data1.2/occs/list.csv?datainfo&rowcount&base_name=mammal

3) What is the appropriate URL for downloading all opinions on the order Testudines in the Mesozoic?
https://training.paleobiodb.org/data1.2/taxa/opinions.csv?datainfo&rowcount&base_name=Testudines&interval=Mesozoic

4) What is the appropriate URL for downloading all collections of Aves, Marsupialia, and Sirenia in the United States as a csv?
https://training.paleobiodb.org/data1.2/colls/list.csv?datainfo&rowcount&base_name=Aves, Marsupialia, Sirenia&cc=US

5) What is the appropriate URL for downloading all occurrences of the gastropod genus Ficus as a csv?
https://training.paleobiodb.org/data1.2/occs/list.csv?datainfo&rowcount&base_name=Ficus&taxon_reso=genus

> You need to specify Gastropoda:Ficus to get just the snail Ficus, not the plant Ficus. -1 Points

## Questions 4

1) What family does the genus Gastrocopta belong to?
Gastrocoptidae

2) There is only once occurrence of Isoetes in Portugal. What age is it?
Aptian

3) What is the age of the oldest occurrence of Gastrocopta?
Bridgerian

4) There is only one occurrence of Tiktaalik in the Paleobiology Database? Was that occurrence located in the tropics or the extratropics when it was alive?
In the tropics

5) There are two occurrences of Namacalathus in Sibera. What geologic formations are they found in?
Kotodzha Formation
Raiga Formation

## Questions 5

1) In Lab Exercise 2 you downloaded a csv file of ammonite sizes from a github URL directly into R.What code would you use to download the above PBDB data directly into R?
````R
> URL<-"https://paleobiodb.org/data1.2/colls/list.csv?base_name=Mammut&interval=Pliocene"
> Pliocene<-read.csv(URL,row.names=1)
````

2) Download the above data into R. What are its dimensions?

````R
> dim(Pliocene)
[1] 39 12
````

3) Did the above call use the occurrences, collections, references, opinions, or specimens route?
Collections

4. What genus is being called for? What is its colloquial name? What age did I limit the data query too?
Mammut
Mastodons
Pliocene

5) Look through the service documentation for the appropriate route (based on your answer to Question 2). Find out how to extend the age search to range from the Miocene Epoch through to the Pleistocene Epoch. Give the new data query URL.
````R
> URL<-"https://paleobiodb.org/data1.2/occs/list.csv?base_name=Mammut&interval=Pleistocene,Miocene”
````

6) I want the data query to show me the paleocoordinates (i.e., paleolatitude and paleolongitude) of each data point. Give the updated data query URL.
````R
> URL<-"https://paleobiodb.org/data1.2/occs/list.csv?datainfo&rowcount&base_name=Mammut&interval=Pleistocene,Miocene&show=paleoloc”
````

## Question 6

1) Write an R function that will take a taxonomic name (as a character string) and an interval (as a character string) as its argument, and will download all fossil occurrences into R. See above.
DataPBDB<-downloadPBDB(Taxa=c("Bivalvia","Gastropoda"),StartInterval="Cambrian",StopInterval="Pleistocene")

> -2 Points

````R
# Like this
downloadPBDB<-function(taxon,interval) {
    URL<-paste("https://training.paleobiodb.org/data1.2/occs/list.csv?datainfo&rowcount&base_name",taxon,"&interval=",interval,sep="")
    return(read.csv(URL))
    }
````

1) Each of the ammonite specimens in Part I of Lab 2 belongs to one of these three species. Based on 1) the morphologic information on these three species in the Paleobiology Database and 2) the morphologic information from Lab 2, can you tell which specimens belong to which species? Explain your reasoning.
Based on WD and comparing it with the the shell width and shell diameter and also the ribbing:
Glyptophiceras sinuatum specimens(moderate to defined ribbing and low WD):8,4,25,19,16,7,9,10,22
Xenoceltites variocostatus specimens(moderate to defined ribbing and high WD):1,2,3,12,13,15,17,18,20,21,11,6
Submeekoceras mushbachanum specimens(undefined ribbing and high WD):23,14,5,

2. Look up Xenoceltites variocostatus in the Paleobiology Database. Find the first person (journal paper/reference) to name this species. (Hint: Both the first and second author's last names start with "B"). What is the name of the article?
A. Brayard and H. Bucher (2008)
Smithian (Early Triassic) ammonoid faunas from northwestern Guangxi (South China): taxonomy and biochronology. Fossils and Strata 55:1-179

3. Do a google scholar search for this article. Open it and scroll down to the "Plates" subsection. You should see various pictures of different ammonites towards the very end of the article. Find the pictures of Xenoceltites variocostatus. Based on the features in these pictures, can you identify which specimens in Part I of Lab 2 belong to this species?
1,2,3,12,13,15,17,18,20,21,25,6

> YOu didn't explain why you made these assignments -1 points.
