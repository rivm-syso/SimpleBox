# SimpleBox4plastic xl_version

This repository provides the spreadsheet version of SimpleBox4plastic.

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7416252.svg)](https://doi.org/10.5281/zenodo.7416252)

## About

SimpleBox4.0-plastic is a variant of the SimpleBox model, which is designed such that it simulates the specific environmental behaviour of nano- and micromaterials, plastics in particular. The model is based on SimpleBox4nano which added three particulate chemical species to the dissolved species already included in SimpleBox. SimpleBox4.0-plastic calculates mass flows of nano- and microplastics (NMP) by simultaneously solving mass balance equations for 4 different chemical species for each environmental compartment in the model.

## Method
SimpleBox4plastic is based on SimpleBox4nano (Quik et al. 2022, submitted). Further documentation on SimpleBox4nano is also available [here](http://rivm.nl/en/Documents_and_publications/Scientific/Scientific_Articles/2014/april/Multimedia_Modeling_of_Engineered_Nanoparticles_with_SimpleBox4nano_Model_Definition_and_Evaluation).

## Model code

SimpleBox is operated as Microsoft Excel spreadsheet, supported by numerical computations in R for quasi-dynamic (level IV) calculations. The preferred option to do this is reading in the spreadsheet model into R and performing further analysis in R. This can be done using the simple R script provided [here](https://github.com/rivm-syso/SimpleBox/blob/master/Dynamic_RShell.md).

## Framework

SimpleBox has served as 'regional distribution module' in the European Union System for the Evaluation of Substances (EUSES). It is currently used as part of the CHESAR tool, hosted by the European Chemicals Agency [[5](http://rivm.nl/en/Documents_and_publications/Common_and_Present/Publications/Guidance_on_information_requirements_and_chemical_safety_assessment_Chapter_R_16_Environmental_Exposure_Estimation "Guidance on information requirements and chemical safety assessment: Chapter R.16 Environmental Exposure Estimation")] to demonstrate possibilities for 'safe use' of chemicals, which is required for registration of chemical substances under REACH. SimpleBox also serves as fate module in Life Cycle Impact Assessment models [[6](http://rivm.nl/en/Documents_and_publications/Scientific/Scientific_Articles/2011/juli/USEtox_human_exposure_and_toxicity_factors_for_comparative_assessment_of_toxic_emissions_in_life_cycle_analysis_Sensitivity_to_key_chemical_properties "USEtox human exposure and toxicity factors for comparative assessment of toxic emissions in life cycle analysis: Sensitivity to key chemical properties")].

Designed originally as a research tool, SimpleBox has proven most useful in dedicated environmental fate studies, focused at understanding and predicting environmental fate from fundamental physical and chemical substance properties.

## Performing quasi-dynamic ('level IV') calculations

SimpleBox uses R-based numeric calculations to produce quasi-dynamic ('level IV') solutions; R/Rstudio installation necessary. SimpleBox calculates steady-state ('level III') output, using Excel only; no R tools are required.

Required: [R](https://www.r-project.org/) and packages [deSolve](https://cran.r-project.org/package=deSolve) and [openxlsx](https://cran.r-project.org/package=openxlsx).

See R notebook: [Dynamic_SB4_Rnotebook.md](https://github.com/rivm-syso/SimpleBox/blob/master/Dynamic_RShell.md).

The RExcell method is depricated.

## Citation

RIVM, 2022. SimpleBox. <https://doi.org/10.5281/zenodo.5743268>

Quik, J.T.K., Meesters, J.A.J. and Koelmans, A.A., 2022. A Multimedia model for microplastic particles. Submitted. [pre-print?]
