# Alberta bird models using ABMI+BAM+BBS data

> Verion 2020

*The code in this repo originates from the <https://github.com/psolymos/abmianalytics> project.*

## What you can find here

This repository contains code to reproduce the 2020 version of Alberta bird models presented on the ABMI data and mapping portals.

The numbered R scripts are the distinct steps in the process (functions that all steps might need, data processing, data packaging, model summaries, prediction/mapping).

The `cc` folder contains code to run the models on WestGrid computing cluster.

The `sector-effects` folder contains code for calculating sector effects with partial backfilling.

## The workflow

1. Combine all the data inputs into a common format (`01-data-processing.R`):
  - species data: BAM and BBS species code can be found in the [borealbirds](https://github.com/borealbirds) organization, ABMI data processing is documented in the [ABbiodiversity/abmidata](https://github.com/ABbiodiversity/abmidata) repo
  - Veg/soil/HF info: [ABbiodiversity/veg-hf-soil-summaries](https://github.com/ABbiodiversity/veg-hf-soil-summaries) repo
  - QPAD offsets: [borealbirds/qpad-offsets](https://github.com/borealbirds/qpad-offsets) repo
  - Lookup tables, etc.: [ABbiodiversity/abmianalytics](https://github.com/ABbiodiversity/abmianalytics), inside the `lookup` folder
2. Create a _data package_ that can be copied over to other machines to run the models (north, south separately) (`02-data-packaging.R`):
  - Various ID, methods related variables (ARU, ROAD, date/time etc), spatial predictors, veg/soil/HF info at various scales
  - Species matrix
  - Offsets matrix
  - Models list
  - Matrix with bootstrap indices
3. Run models and save the output for each species (scripts in the `cc` folder: these will run locally or on a cumpute cluster)
4. Check results (`03-model-summaries.R`)
5. Prediction maps, sector effects, figures, etc. are described in the `pipeline/2020` folder of the [ABbiodiversity/abmianalytics](https://github.com/ABbiodiversity/abmianalytics/) repo.
6. Final coefficients are wrapped in the [ABbiodiversity/allinone](https://github.com/ABbiodiversity/allinone) and [ABbiodiversity/allinone-coefs](https://github.com/ABbiodiversity/allinone-coefs)repos for easy distribution and reproducibility.

