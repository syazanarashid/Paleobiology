Tuan Syazana Tuan Ab Rashid
Lab 9 - due April 4,2016
The migration of paleocontinents

> Thank you for formatting it so well! 20/20

## Problem Set 1

1) Is North America currently (i.e., in the present) to the West or East of its position in the Cretaceous?

To the West of its position in the Cretaceous.

2) Look at the following line of code that you used before.

````R
plot(ModernMap,col=rgb(1,0,0,0.33),lty=0,add=TRUE)
Describe what this code is doing. A good answer will describe what each of the plot( ) function arguments is doing - i.e., what is the meaning of col=, lty= and add=. As well, what does the rgb( ) function do? What does it mean? Use google or the R help( ) function.
````

plot( )
Generic function for plotting of R objects.

col
The colors for lines and points. Multiple colors can be specified so that each point can be given its own color. If there are fewer colors than points they are recycled in the standard fashion. Lines will all be plotted in the first colour specified.

lty
a vector of line types

add	
logical; if TRUE add to an already existing plot; if NA start a new plot taking the defaults for the limits and log-scaling of the x-axis from the previous plot. Taken as FALSE (with a warning if a different value is supplied) if no graphics device is open.

rgb( )
This function creates colors corresponding to the given intensities (between 0 and max) of the red, green and blue primaries. The colour specification refers to the standard sRGB colorspace (IEC standard 61966).

3) Download a map of the middle Cretaceous (Albian Epochs ~110 mys ago). Name it AlbianMap.

````R
> # Download an Albian map
> AlbianMap<-downloadPaleogeography(Age=110)
````

4) Add AlbianMap to the plot you made earlier. The added continents should be colored green, and use the same level of opacity (translucence) as your CretaceousMap and ModernMap. Show your code!

````R
> plot(AlbianMap,col=rgb(0,1,0.1,0.33),lty=0,add=TRUE)
````

5) Has there been more movement north and south or east and west in the Eastern Hemisphere since the Albian?

Movement North and East in the Eastern Hemisphere since the Albian.

6) Has there been more movement north and south or east and west in the Western hemisphere since the Albian?

Movement to the west in the Western hemisphere since the Albian.

## Problem Set 2

1) Download and plot a new map of the Paleocene/Eocene boundary (Use google to find the age of this boundary, remember the downloadMap( ) function only takes whole numbers). You may use any color and level of opacity. Show your code.

````R
> # Download an Paleocene/Eocene boundary map
> PaleoceneEoceneMap<-downloadPaleogeography(Age=56)
> plot(PaleoceneEoceneMap,col=rgb(0,1,0.1,0.33),lty=0)
````

2) Download a dataset of Anthozoan occurrences from the paleobiology database ranging from the Paleocene through Eocene. Consult with previous labs if you do not remember how to do this. Show your code.

````R
> DataPBDB<-downloadPBDB(Taxa=c("Anthozoa"),StartInterval="Paleocene",StopInterval="Eocene")
````

3) How many occurences did you download?

````R
> nrow(DataPBDB)
[1] 2847
````

4) What are the names of columns of the PBDB data matrix you just downloaded. What does each column mean? If you do not know, consult with the API documentation.

````R
> colnames(DataPBDB)
 [1] "occurrence_no"   "record_type"     "reid_no"         "flags"           "collection_no"  
 [6] "identified_name" "identified_rank" "identified_no"   "difference"      "accepted_name"  
[11] "accepted_rank"   "accepted_no"     "early_interval"  "late_interval"   "max_ma"         
[16] "min_ma"          "reference_no"    "paleomodel"      "paleolng"        "paleolat"       
[21] "geoplate"        "phylum"          "class"           "order"           "family"         
[26] "genus"        

"occurrence_no"
A positive integer that uniquely identifies the occurrence

"record_type"
The type of this object: occ for an occurrence.

"reid_no"
If this occurrence was reidentified, a unique identifier for the reidentification. This value is a key for the reidentification table, and is probably useful only for debugging purposes. It does, at least, indicate that this was not the original identification of the occurrence.

"flags"
This field will be empty for most records. A record representing an identification that has been superceded by a more recent identification will have the letter R in this field.

"collection_no"
The identifier of the collection with which this occurrence is associated.

"identified_name" 
The taxonomic name by which this occurrence was identified. This field will be omitted for responses in the compact voabulary if it is identical to the value of accepted_name.

"identified_rank" 
The taxonomic rank of the identified name, if this can be determined. This field will be omitted for responses in the compact voabulary if it is identical to the value of accepted_rank.

"identified_no"   
The unique identifier of the identified taxonomic name. If this is empty, then the name was never entered into the taxonomic hierarchy stored in this database and we have no further information about the classification of this occurrence. In some cases, the genus has been entered into the taxonomic hierarchy but not the species. This field will be omitted for responses in the compact voabulary if it is identical to the value of accepted_no.

"difference"
If the identified name is different from the accepted name, this field gives the reason why. This field will be present if, for example, the identified name is a junior synonym or nomen dubium, or if the species has been recombined, or if the identification is misspelled.      

"accepted_name"
The value of this field will be the accepted taxonomic name corresponding to the identified name.

"accepted_rank"   
The taxonomic rank of the accepted name. This may be different from the identified rank if the identified name is a nomen dubium or otherwise invalid, or if the identified name has not been fully entered into the taxonomic hierarchy of this database.

"accepted_no"     
The unique identifier of the accepted taxonomic name in this database.

"early_interval"  
The specific geologic time range associated with this occurrence (not necessarily a standard interval), or the interval that begins the range if late_interval is also given

"late_interval"   
The interval that ends the specific geologic time range associated with this occurrence, if different from the value of early_interval

"max_ma"
The early bound of the geologic time range associated with this occurrence (in Ma)

"min_ma"          
The late bound of the geologic time range associated with this occurrence (in Ma)

"reference_no"    
The identifier of the reference from which this data was entered

"paleomodel"      
The primary model specified by the parameter pgm. This field will only be included if more than one model is indicated.

"paleolng"    
The paleolongitude of the collection, evaluated according to the primary model indicated by the parameter pgm.    

"paleolat"
The paleolatitude of the collection, evaluated according to the primary model indicated by the parameter pgm.

"geoplate"        
The identifier of the geological plate on which the collection lies, evaluated according to the primary model indicated by the parameter pgm. This might be either a number or a string.

"phylum"          
The name of the phylum in which this occurrence is classified.

"class"           
The name of the class in which this occurrence is classified.

"order"           
The name of the order in which this occurrence is classified.

"family"
The name of the family in which this occurrence is classified.

"genus"
The name of the genus in which this occurrence is classified. If the block subgenus is specified, this will include the subgenus name if any.
````

5) Use the points( ) function to plot each occurrence on the map you made previously (make sure to use the paleolatitude and paleolongitude coordinates). Show your code. If you do not know how to use the points( ) function, consult the help file or use Google.

````R
> plot(PaleoceneEoceneMap,col=rgb(0,1,0.1,0.33),lty=0)
> points(DataPBDB[ ,"paleolng"],DataPBDB[ ,"paleolat"])
````

6) Where are most of the Anthozoan occurrences in the Eastern Hemisphere (i.e., what region of the world)? Are Anthozoans primarily marine or freshwater organisms? What can you infer must have existed in this region of the world during this time?

Anthozoan occurances are mostly in the Europe and Turkey region. They are primarily marine organisms so this region must have been a marine environment during this time. 

## Problem Set 3

1) Download a dataset of Perissodactyla occurrences from the PBDB that span the Paleogene. Show your code.

````R
> DataPBDB<-downloadPBDB(Taxa=c("Perissodactyla"),StartInterval="Paleocene",StopInterval="Oligocene")
````

2) What is the defining attribute of Perissodactyla? What are some prominent examples (e.g., lions, tigers, bears, oh my!)? [Hint: Neither lions, nor tigers, nor bears are members of Perissodactyla.]

The defining attribute of Perissodactyla is the possession of either one or three hoofed toes on each hindfoot

Examples: horses, zebras, tapirs, rhinoceroses

3) Find collection number 112723 in the dataset you just downloaded in Question 1. Show your code.

````R
> which(DataPBDB[,"collection_no"]==112723)
[1] 3548 3550
> DataPBDB[3548,]
     occurrence_no record_type reid_no flags collection_no          identified_name identified_rank identified_no difference
3548        961980         occ      NA    NA        112723 Eotitanops pakistanensis         species        169823           
                accepted_name accepted_rank accepted_no early_interval late_interval max_ma min_ma reference_no paleomodel paleolng
3548 Eotitanops pakistanensis       species      169823       Ypresian                   56   47.8        36699     gp_mid     70.7
     paleolat geoplate   phylum    class          order          family      genus
3548     2.76      501 Chordata Mammalia Perissodactyla Brontotheriidae Eotitanops
> DataPBDB[3550,]
     occurrence_no record_type reid_no flags collection_no      identified_name identified_rank identified_no difference
3550        963172         occ      NA    NA        112723 Balochititanops haqi         species        192106           
            accepted_name accepted_rank accepted_no early_interval late_interval max_ma min_ma reference_no paleomodel paleolng paleolat
3550 Balochititanops haqi       species      192106       Ypresian                   56   47.8        36699     gp_mid     70.7     2.76
     geoplate   phylum    class          order          family           genus
3550      501 Chordata Mammalia Perissodactyla Brontotheriidae Balochititanops
````

4) What "geoplate" id (tectonic plate) is associated with this collection? What modern day region of the world does this geoplate id correspond to? The remaining questions will refer to this geoplate/region as region-X.

Geoplate id 501, which correspond to modern day Pakistan.

5) Subset your dataset of Perissodactyla occurrences to only include occurrences that occur in region-X. How many occurrences are there? Show your code.

````R
> Peri501<-subset(DataPBDB,DataPBDB[,"geoplate"]=="501")
> nrow(Peri501)
[1] 84
````

6) Using the maps we have created previously, making your own new maps, or using the Paleobiology Database Navigator tool, what is the general history of region-X from the Albian through to the present day?

The eastern part of Pakistan is part of the Eurasian plate and the western part of Pakistan is part of the Indian plate. The Indian Plate migrated North and eventually collided with the Eurasian plate.

7) There are also many Paleogene occurrences of Perissodactyla in present day China. Using the maps we have created previously, making your own new maps, or using the Paleobiology Navigator tool, evaluate the plausibility of each of the following scenarios? Thoroughly explain your reasoning and how you tested your ideas.

Species of Perissodactyla migrated from region-X to China during the Paleogene?
Not possible, (unless their fossils in Pakistan were not preserved and found), since Pakistan was surrounded by sea when there was already occurences of Perissodactyla in other parts of the world such as North America and China. I compared the continent configurations and occurences on the Paleobiology Database Navigator.

Species of Perissodactyla migrated from China to region-X during the Paleogene?
Possible, since there was first an occurence of Perissodactyla in China during the Paleocene, followed by even more occurances there during the Eocene, including a trail of occurences between China and Pakistan. This coincides with the connecting continents that are no longer separated by big seas. I compared the continent configurations and occurences on the Paleobiology Database Navigator.

The species of Perissodactyla in China and region-X are unrelated and probably both came from a third region?
I think the species in both region are related, but before it got to china and to Pakistan, it might have first come from North America. I looked at each of the available continent configurations on the Paleobiology Database Navigator and saw that the Perissodactyla were mostly present on the North American Plate with some found north of China.

