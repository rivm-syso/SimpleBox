# SimpleBox4nano xl_version

This repository provides the spreadsheet version of SimpleBox4plastic.

[![](https://zenodo.org/badge/DOI/10.5281/zenodo.10671831.svg)](https://doi.org/10.5281/zenodo.10671831)

## About

SimpleBox4.0-nano is a variant of the SimpleBox model, which is designed such that it simulates the specific environmental behaviour of nanomaterials. The main adaptation consists of adding three particulate chemical species[^readme-1] to the dissolved species already included in SimpleBox. SimpleBox4.0-nano calculates mass flows of nanomaterials by simultaneously solving mass balance equations for 4 different chemical species for each environmental compartment in the model.

[^readme-1]: The three particulate chemical species consist of: i) the emitted nanomaterial, ii) smaller heteroagglomerates (\<450 nm) consisting of nanomaterial and natural colloids or aerosols and iii) bigger heteroagglomerates (\>450 nm) consisting of nanomaterials and other particulates found in air, water and soil.

## Method

Documentation on the model definition that is added to simplebox to include the three particulate chemical species and make the model fit for nano has been published [[1](http://rivm.nl/en/Documents_and_publications/Scientific/Scientific_Articles/2014/april/Multimedia_Modeling_of_Engineered_Nanoparticles_with_SimpleBox4nano_Model_Definition_and_Evaluation)]. The main input parameters related to nanomaterial fate are the size and density of the nanomaterial, the size, density and concentration of natural particles and the transformation rates from emitted nanomaterial to the heteroagglomerate or dissolved species.

## Model code

SimpleBox is operated as Microsoft Excel spreadsheet, supported by numerical computations in R for quasi-dynamic (level IV) calculations. The preferred option to do this is reading in the spreadsheet model into R and performing further analysis in R. This can be done using the simple R script provided [here](https://github.com/rivm-syso/SimpleBox/blob/master/Dynamic_RShell.md).

## Framework

SimpleBox has served as 'regional distribution module' in the European Union System for the Evaluation of Substances (EUSES). It is currently used as part of the CHESAR tool, hosted by the European Chemicals Agency [[2](http://rivm.nl/en/Documents_and_publications/Common_and_Present/Publications/Guidance_on_information_requirements_and_chemical_safety_assessment_Chapter_R_16_Environmental_Exposure_Estimation "Guidance on information requirements and chemical safety assessment: Chapter R.16 Environmental Exposure Estimation")] to demonstrate possibilities for 'safe use' of chemicals, which is required for registration of chemical substances under REACH. SimpleBox also serves as fate module in Life Cycle Impact Assessment models [[3](http://rivm.nl/en/Documents_and_publications/Scientific/Scientific_Articles/2011/juli/USEtox_human_exposure_and_toxicity_factors_for_comparative_assessment_of_toxic_emissions_in_life_cycle_analysis_Sensitivity_to_key_chemical_properties "USEtox human exposure and toxicity factors for comparative assessment of toxic emissions in life cycle analysis: Sensitivity to key chemical properties")].

Designed originally as a research tool, SimpleBox has proven most useful in dedicated environmental fate studies, focused at understanding and predicting environmental fate from fundamental physical and chemical substance properties.

## Performing quasi-dynamic ('level IV') calculations

SimpleBox uses R-based numeric calculations to produce quasi-dynamic ('level IV') solutions; R/Rstudio installation necessary. SimpleBox calculates steady-state ('level III') output, using Excel only; no R tools are required.

Required: [R](https://www.r-project.org/) and packages [deSolve](https://cran.r-project.org/package=deSolve) and [openxlsx](https://cran.r-project.org/package=openxlsx).

See R notebook: [Dynamic_SB4_Rnotebook.md](https://github.com/rivm-syso/SimpleBox/blob/master/Dynamic_RShell.md).

## Citation

RIVM, 2024. SimpleBox. <https://doi.org/10.5281/zenodo.5743268>

Meesters, J.A.J., Koelmans, A.A., Quik, J.T.K., Hendriks, A.J., van de Meent, D., 2014. Multimedia Modeling of Engineered Nanoparticles with SimpleBox4nano: Model Definition and Evaluation. Environmental Science & Technology 48, 5726--5736. <https://doi.org/10.1021/es500548h>
