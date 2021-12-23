# SimpleBox xl_version

This repository provides the spreadsheet version of SimpleBox.

## About

![Nested scales SimpleBox](https://www.rivm.nl/sites/default/files/2018-11/Illustratie%2520Simplebox%25204.jpg "Nested scales SimpleBox")

SimpleBox is a multimedia mass balance model of the so-called 'Mackay type'. It simulates environmental fate of chemicals as fluxes (mass flows) between a series of well-mixed boxes of air, water, sediment and soil on regional, continental and global spatial scales.

## Method

SimpleBox does so by simultaneously solving mass balance equations for each environmental
compartment box in the model. SimpleBox is a first-principles model in the sense that it internally derives mass flow rates from physical and chemical substance properties, and characteristics of the environment modeled. It takes user-specified release rates as input, producing exposure concentrations in the environment as output.

## Model code

SimpleBox is operated as Microsoft Excel spreadsheet, supported by numerical computations in R, which are linked to the spreadsheet via RExcel. Documentation has been published for model versions 1-4 in various technical RIVM documents [[1](https://www.rivm.nl/publicaties/simplebox-a-generic-multimedia-fate-evaluation-model "SIMPLEBOX: a generic multimedia fate evaluation model"), [2](https://www.rivm.nl/bibliotheek/rapporten/719101029.html "SimpleBox 2.0: a nested multimedia fate model for evaluating the environmental fate of chemicals"), [3](https://www.rivm.nl/en/simplebox-30-multimedia-mass-balance-model-for-evaluating-fate-of-chemical-in-environment "SimpleBox 3.0: Multimedia mass balance model for evaluating the fate of chemical in the environment"), [4](https://www.rivm.nl/bibliotheek/rapporten/2015-0161.pdf "SimpleBox 4.0 : A multimedia mass balance model for evaluating the fate of chemical substances")].

## Framework

SimpleBox has served as 'regional distribution module' in the European Union System for the
Evaluation of Substances (EUSES). It is currently used as part of the CHESAR tool, hosted by the European Chemicals Agency [[5](http://rivm.nl/en/Documents_and_publications/Common_and_Present/Publications/Guidance_on_information_requirements_and_chemical_safety_assessment_Chapter_R_16_Environmental_Exposure_Estimation "Guidance on information requirements and chemical safety assessment: Chapter R.16 Environmental Exposure Estimation")] to demonstrate possibilities for 'safe use' of chemicals, which is required for registration of chemical substances under REACH. SimpleBox also serves as fate module in Life Cycle Impact Assessment models [[6](http://rivm.nl/en/Documents_and_publications/Scientific/Scientific_Articles/2011/juli/USEtox_human_exposure_and_toxicity_factors_for_comparative_assessment_of_toxic_emissions_in_life_cycle_analysis_Sensitivity_to_key_chemical_properties "USEtox human exposure and toxicity factors for comparative assessment of toxic emissions in life cycle analysis: Sensitivity to key chemical properties")].

Designed originally as a research tool, SimpleBox has proven most useful in dedicated environmental fate studies, focused at understanding and predicting environmental fate from fundamental physical and chemical substance properties.

## Performing quasi-dynamic ('level IV') calculations

SimpleBox uses R-based numeric calculations to produce quasi-dynamic ('level IV') solutions; R/Rstudio installation necessary. SimpleBox calculates steady-state ('level III') output, using Excel only; no R tools are required.

Required: [R](https://www.r-project.org/) and packages [deSolve](https://cran.r-project.org/package=deSolve) and [openxlsx](https://cran.r-project.org/package=openxlsx).

See R notebook: [Dynamic_SB4_Rnotebook.md](https://github.com/rivm-syso/SimpleBox/blob/master/Dynamic_RShell.md).

The RExcell method is depricated.

## Citation

...
