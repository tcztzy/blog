# Recombination rate estimation

## Introduction

There are three major methods to estimate recombination rates@@penalba2020 :

1. Population-based
2. Pedigree-based
3. Gamete-based

## Population-based methods

Population-based methods use genetic variation data from a population to estimate recombination rates.
Typically, these methods use 10-30 samples from a population to estimate recombination rates. Programs such as LDhat, LDhelmet, and fastEPRR are popular population-based methods.
The advantage of population-based methods is that they can estimate recombination rates at a fine scale, but the disadvantage is that they require numerous samples to obtain accurate estimates, and they are sensitive to the demographic history of the population/selection and mutation. The genome assembly quality also highly affects the accuracy of the estimation.

Pedigree and gamete-based methods are not covered in this note, since currently I am not working on them.

| Program | Description | Reference |
| ------- | ----------- | --------- |
| LDhat   | A package for the analysis of recombination rates from population genetic data | @@auton2007 |
| LDhelmet | A program for estimating recombination rates and detecting selective sweeps from population genetic data | @@chan2012 |
| pyrho | a fast demography-aware inference of fine-scale recombination rates based on fused-LASSO | @@spence2019 |
| fastEPRR | A fast and accurate method to estimate recombination rates | @@gao2016 |

## LDhat

LDhat@@auton2007 is a popular population-based method to estimate recombination rates.
