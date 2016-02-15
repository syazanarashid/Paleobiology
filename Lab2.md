<p>Tuan Syazana Tuan Ab Rashid</p>
<p>Paleobiology</p>
<p>Lab 2 - due Feb 8, 2016</p>

> Final grade 19/20

## Part I

1) Your identifications (how many species do you recognize in the group, and which specimens belong to which species). Explain how and why you came to this conclusion.

I identified three different species based on the degree of definition of their ornamentation and also by how much it spirals.

````R
# Species 1 has well-defined ribbing on the outer shell and spirals a few times.
Species1<-Ammonites[c(1,8,11,20,21,6,2,18,4,12),]
# Species2 has low-defined ribbing on the outer shell, widens out pretty soon at the end of the chamber without as many spirals.
Species2<-Ammonites[c(16,23,25,14,5,19),]
# Species3 have moderate to low-defined ribbing on the outer shell and spirals a few times.
Species3<-Ammonites[c(15,7,22,3,9,10,13,24,17),]
````

2) The morphological features you used to distinguish each species, including whatever combination of qualitative or quantitative traits you think are important.

I identified the three different species based on the degree of definition of their ornamentation and also by how much it spirals.

3) The nature of ontogenetic change, if any, in the species. Explain your reasoning.

> Great hypotheses

In Species1, the nature of ontogenic change in the species is characterized by the closeness of their ribbing. The juveniles would have more spaced out ribbing whereas the adult would have more closely spaced ribbing. The adult would also have more, if any, growth lines. This is noticable in comparing between specimen 11 and 21. Also, the adults would have more spiralling, corresponding to their older age.

In Species2, the nature of ontogenic change in the species is characterized by the number of spiraling of the shell. The adults would have more spiralling, corresponding to their older age.

In Species3, the nature of ontogenic change in the species is characterized by the number of spiraling of the shell. The adults would have more spiralling, corresponding to their older age.

4) The possibility of sexual dimorphism as a cause of morphological differences and how you evaluated that possibility.

Some of the smaller specimens in the species still have a lot of spiralling and well-defined ribbing, which might indicate that it is still an adult, so the morphological difference then may be caused by sexual dimorphism. That is, the larger D for each species is the females since females require a larger body size for egg production.

## Part II

#### Subsection 1

1) Each element of the plethodon list has a name. What are they?

````R
> objects(plethodon)
> "land" "links" "species" "site" "outline"
````

> You could also use names
````R
names(plethodon)
````

2. What class is each object?

````R
> class(plethodon)
[1] "list"
````

3. What are the dimensions of the first object in the plethodon list?

> - 0.25 points

````R
> MyArray<-(plethodon["land"])
> dim(MyArray)
> 1
````

> You came close, but you need to use 
````R
[[ ]]
```` 
when working with a list.
````
dim(plethodon[["land"]])
[1] 12  2 40
````

#### Subsection 2

1) Use the hummingbird dataset. Which object in the list records the landmark data?

"land"

2) Perform a procrustes on the landmark data.

````R
#Procrustes analysis is a form of statistical shape analysis used to analyse the distribution of a set of shapes.
> ProcrustesHummingbirds<-gpagen(hummingbirds[["land"]])
> ProcrustesHummingbirds
````

3) Perform a PCA on the hummingbird data.
#Principal Components Analysis

````R
plotTangentSpace(ProcrustesHummingbirds[["coords"]],warpgrids=FALSE,verbose=FALSE)
````

4. How many "species" of hummingbird are there?

> You did not explain why you came to this number. -0.5 points

1

## Part III

1) What is the synapomorphy of the clade containing species D and E?

Fangs longer than 6 inches

2)  What is a plesiomorphic character of that clade?

Sulfurous odor

3) What is the synapomorphy of the clade containing species A and B?

Adorable eyelashes

4) Which taxa have a sulfurous odor?

C, D, and E

5) What character distinguishes species D from species E?

Laser death ray

6) Are adorable eyelashes a synapomorphy or an autapomorphy?

Synapomorphy

7) Traditionally, the five taxa are grouped into three families. Determine if each family is monophyletic, paraphyletic, or polyphyletic.

> -0.25 points

+ Family 1: contains species A -> <strike>paraphyletic</strike> monophyletic
+ Family 2: Contains species B and C -> polyphyletic
+ Family 3: contains species D and E -> monophyletic

8)  More recently, species A has been grouped in a family with species D and E. Is this advisable? Why or why not?

No, because they do not share the same synapomorphy (shared derived characteristics)

9) Determine if the following groups are monophyletic, paraphyletic, or polyphyletic.

> -0.25 points

+ Group 1: Species A, B, C -> paraphyletic
+ Group 2: Species C, D, E -> <strike>monophyletic</strike> polyphyletic
+ Group 3: Species C and D -> paraphyletic
+ Group 4: Species A and B -> monophyletic
+ Group 5: Species B, D, E -> polyphyletic

Part IV
1. Assuming that Gryphaea arcuata represents the ancestor, what type of heterochrony is most likely responsible for evolution of these two species?
Peramorphosis for Gryphaea mccullochi (D) and Paedomorphosis for Gryphaea gigantea (E). 

2. Which species of Gryphaea has undergone a greater degree of heterochrony?
Gryphaea mccullochi (D)

3. What type of heterochrony is represented in the Olenellus example?
Paedomorphosis
