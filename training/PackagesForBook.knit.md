---
author:
  - "Eliot McIntire"
date: last-modified
editor_options:
  chunk_output_type: console
---


# R packages for book

The objective of this book is to facilitate lightweight project code. To do this, packages and any code that are used must be easy to install and use. As a result, under most circumstances, users don't need to "pre-install" packages because each chapter will install its own packages. Furthermore, packages, once installed for one project, will be cached locally so that the next project will be able to install quickly from local package cache. We have attempted to allow all sections to be run without administrator priviledges. 

# Common setup

If you can run the following code, then you will be able to run code in any of the chapters in this book. This code installs a few packages (notably `SpaDES.project` and `Require` and their dependencies), then it downloads and installs a single SpaDES module. This module happens to have many package dependencies (over 130 packages). 


::: {.cell}

```{.r .cell-code}
install.packages("SpaDES.project", 
                 repos = c("predictiveecology.r-universe.dev", 
                           getOption("repos")), dependencies = TRUE)

library(SpaDES.project)
out <- setupProject(
  name = "Introduction",
  modules = "PredictiveEcology/Biomass_core@main",
  packages = "disk.frame"
)
```
:::



## See also

@sec-TroubleShoot

