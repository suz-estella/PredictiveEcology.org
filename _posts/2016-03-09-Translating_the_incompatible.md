---
layout: post
title: Removing spaghetti from ecological models
author: Eliot McIntire
date: March 9, 2016
tags: [SpaDES, modules, modularity, sketch]
comments: true
---

## What if modules are not compatible?

Continuing from previous post on [modularity](http://predictiveecology.org/2016/03/09/Removing_spaghetti_from_ecological_models.html), the next issue, of course, is not every module will be compatible out of the box. If we continue with the example from last post, not every growth module will take "stem counts and size by species". One solution to this is the idea of **translator modules**. 

## Translator modules

These will create 3 situations:

- lossy translators
- lossless translators
- incompatible

In cases where there is no possible translation between data types or formats, then we are out of luck. We won't fit every model together... We will likely not ever build a set of translators to connect [SORTIE](http://www.sortie-nd.org/)  with [FORECAST](http://web.forestry.ubc.ca/ecomodels/moddev/forecast/forecast.htm). It certainly would be useful as a hypothesis testing exercise to have them compatible, but that is another entry.  

## Lossy

An example of a lossy translator ... Lossy is like changing a 37 level forest cover classification to a 7 level forest cover classification. We certainly can in principle write this translation... do we always want to? 
Well, who knows a priori. For some purposes, it will be ok to lose some detail in the forest cover classification. Can we go from 7 back to 37?  
Maybe... it depends on a bunch of things. We certainly could do it probabilistically... level 3 becomes 5, 12, 15, and 23 with probabilies 0.1, 0.2, 0.3, and 0.4... or we could do a Bayesian version, where the probability is affected by the prior level of that pixel in the 37 level FC classification (assuming we went from 37 to 7 and now are going back to 37). 
These translations could be data driven, or expert driven or whatever. But, the point is that the translator modules are an easy mechanism to link modules that don't, on the surface, look like they link.

### Examples of lossy

- GIS operations

    - rasterizing a polygon layer
    - reprojecting
    
- Ecological operations

    - reclassifying

## Not always symmetrical

It is important to note that a translator may be lossy in one direction, but the reverse translation will *lossless*. In many cases this is ok. Take for example, if there is a vegetation module that is working with a vegetation layer with 37 classes, and a fire module that can only deal with 7 classes, the sequence would go like this:

- vegetation module works on a raster data layer with 37 classes
- translator translates the 37 to a 7 class layer for input to fire module
- fire module uses the 7 class layer, and converts some of the pixels in the raster to one class ("burned")
- the 2nd translator converts the 7 back to the 37 classes but only for pixels that *changed* because they were burned, but none of the others. 
- 37 class vegetation stays at 37 classes, with some pixels converted to "burned"
- vegetation module continues on 37 class layer **without any loss**

## Lossless

Changing units is a common example
Anyway, these are some of the discussions and plans we are coming up with. I would be happy to include you in these, as often as you are interested.  And other people too. Indeed, we need more people to make better decisions...up to a point ;) 

There are a lot of drawbacks to modularity... but there are a lot of benefits, and for me they are outweighing the drawbacks at the moment.


### Playground
Imagine a neighbourhood where the kids (scientists/ecological modelers) are all playing scattered all over. Some have backyard swings and slides, others don't. They are having a grand old time running around having fun, living life (i.e., collecting data and publishing science). What we have done is build a new playground structure for the neighbourhood kids to play on (SpaDES). As we start to invite them to play, they check it out... some come and bring with them the their backyard play structures (pre-existing modules) that can attach to the structure we built, and others come with just materials to add new structures (new modules). The new games that are played are bigger, cooler, and more exciting than when the kids were playing alone or in small groups.  
