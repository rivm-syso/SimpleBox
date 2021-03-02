---
title: "Rshell for dynamic simplebox"
author: "Joris Quik"
date: "2/14/2020"
output: html_document
editor_options: 
  chunk_output_type: console
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
library(openxlsx)
library(deSolve)
library(ggplot2)
library(reshape2)
```

## Introduction

This document describes the code and functions to produce quasi-dynamic ('levelIV') solutions of the [SimpleBox](https://www.rivm.nl/simplebox) multimedia fate model.

Prerequisites to run this code is a recent version of SimpleBox (Feb. 2020 or later). 
The only relevant change in SimpleBox with the previous version (31-05-2015) is the naming of a vector of compartment names as *box_names*.

This script should work for both SimpleBox (conventional) and SimpleBox4nano.

## preparing data
Define the location of the simplebox xlsx file.
If used in an R project, the default location is the *data* folder.

```{r read in data, echo=TRUE}
sb4n.loc <- "data/SimpleBox4.0_web_PBT1.xlsm"

## NOTE ##
## Sometimes the naming of the cells in excel is different based on the version you are using.
## i.e. check that matrix "K" is the correct name, see worksheet "engine". It could be "Kmatrix"

SB.K <- as.matrix(read.xlsx(sb4n.loc,colNames=FALSE, namedRegion ="Kmatrix")) # matrix of rate constants "k"
SB.m0 <- read.xlsx(sb4n.loc,colNames=FALSE, namedRegion ="m0") # Initial mass of each compartment, could be "m0"
SB.names <- read.xlsx(sb4n.loc,colNames=FALSE, namedRegion ="box_names") #Names for each compartment
SB.v <- read.xlsx(sb4n.loc,colNames=FALSE, namedRegion ="v") #Volumes
SB.e <- read.xlsx(sb4n.loc,colNames=FALSE, namedRegion ="emis") # Emission rates for each
ChemClass <- as.character(read.xlsx(sb4n.loc,colNames=FALSE, namedRegion ="ChemClass")) # Emission rates for each
colnames(SB.v) <- SB.names
colnames(SB.e) <- SB.names

```

The K matrix, starting masses at t=0, emissions vector, the compartment names and compartment volumes are read from the SimpleBox xls file: `r sb4n.loc`.

## Calculation 
The inverse of the matrix of rate constants (K) multiplied with the mass in each compartment (m) plus the emission (e) gives the change in mass of each time step per compartment.

```{r SimpleBoxODE}
# ODE function of SimpleBox:
SimpleBoxODE <- function(t, m, parms) {
  dm <- with(parms, K %*% m + e)
  return(list(dm))
}
```

This function can be used in different ways, here we give an example to calculate the concentrations in time based on 3 chronological emission scenarios: 

```{r define emission scenario}
Period1 <- 20 # in years
Period2 <- 10 # in years
EmisReduc1 <- 50 # percentage emission reduction relative to period 1
Period3 <- 10 # in years
EmisReduc2 <- 100 # percentage emission reduction relative to period 1
```

A helperfunction is applied to calculate the 3 seperate periods. These are then added together to get the raw output which is a matrix of masses in each compartment per time point.

```{r calculate raw output}

# helper function to calculate dynamic output for set time span
Rdyn.base <- function(Parms,    # list of parms needed for SimpleBoxODE fucntion
                      tstart,   # First time point (in seconds)
                      tend,     # Last time point (in seconds)
                      SB.m0,    # Vector of initial masses
                      SB.names, # Vector of compartment names
                      tlength){ # Number of concentrations to output between start and end
  
  tset <- seq(from=tstart, to=tend, length.out=tlength) # make time sequence for which output is wanted
  Rpar.SBdyn <- list(tset=tset, m=as.numeric(SB.m0), parms=Parms)
  
  # Run ODE function to create out1 with masses in each compartment at different time points
  out <- with(Rpar.SBdyn, {
    ode(y=m,times=tset,func=SimpleBoxODE,parms=parms)
  })
  colnames(out)<-c("Time",SB.names)
  
  out
}


tend1 <- 60*60*24*365*Period1 # set this in seconds
SB.e1 <- SB.e            # Emission as read from xlsx model file in sb4n.loc
tlength1 <- tend1/(60*60*24*(365/12))+1 # number of output points (approx. 1 per month)
tend2 <- 60*60*24*365*(Period1+Period2) # set this (seconds)
SB.e2 <- SB.e*(1-EmisReduc1/100)        # 50% emission (can also be set to 0, use rep(0,length(SB.e)))
tlength2 <- (tend2-tend1)/(60*60*24*(365/12))+1 # number of output points (approx. 1 per month)
tend3 <- 60*60*24*365*(Period1+Period2+Period3) # set this (seconds)
SB.e3 <- SB.e*(1-EmisReduc2/100) # emission stops
tlength3 <- (tend3-tend2)/(60*60*24*(365/12))+1 # number of output points (approx. 1 per month)

# calculate mass in each compartment for 3 time spans with different emission regimes make the timeline  
# period 1: 100% emission as input in sb4n.xlsx 

Parms1 <- list(e=SB.e1, K=as.matrix(SB.K))
out.t1 <- Rdyn.base(Parms = Parms1,
                    tstart = 0, 
                    tend = tend1,
                    SB.m0=SB.m0,
                    SB.names,
                    tlength = tlength1)

# period 2: 50% emission
Parms2 <- list(e=SB.e2, K=as.matrix(SB.K))
out.t2 <-  Rdyn.base(Parms = Parms2,
                     tstart = tend1,
                     tend = tend2,
                     SB.m0=out.t1[tlength1,-1],
                     SB.names,
                     tlength = tlength2)

# period 3: emission stops
Parms3 <- list(e=SB.e3, K=as.matrix(SB.K))
out.t3 <- Rdyn.base(Parms = Parms3,
                    tstart = tend2,
                    tend = tend3,
                    SB.m0=out.t2[tlength2,-1],
                    SB.names,
                    tlength = tlength3)


out1 <- rbind(out.t1,out.t2,out.t3)

```

