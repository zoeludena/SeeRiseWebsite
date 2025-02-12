---
layout: page
title: Exploratory Data Analysis
permalink: /eda/
---

Our first figure is one of our temperature prediction using the pattern scaling (linear) emulator. We can see it does a good job predicting sea level rise. This follows the paper (TODO).

<iframe src="assets/figures/tas_predict_vs_historical.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

Our second figure is using the pattern scaling (linear) emulator to predict the different Shared Socioeconomic Pathways (SSPs).

<iframe src="assets/figures/tas_preds_ssps.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

Our third figure uses three other emulators. We can see the neural network, gaussian processing model, and random forest model perform slightly different than pattern scaling, but still follow the general expected trend.

<iframe src="assets/figures/tas_preds_ssp245_compare_emulators" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

Our fourth figure plots the NASA projection and uncertainty window, their [Sea Level projection Tool](https://sealevel.nasa.gov/ipcc-ar6-sea-level-projection-tool?type=global). Seen below are the median see level rise predicted every ten years. The shaded ranges show the 17th-83rd percentile ranges for NASA's prediction. The shaded region is based off of a bunch of models that capture a range of uncertainty.

<iframe src="assets/figures/nasa_slr_projection.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

Our fifth figure plots the NASA projection for SSP 245 and the emulators. We can see that we are on the lower range of uncertainty for NASA's prediction. The emulator that performs the best appears to be the gaussian process.

<iframe src="assets/figures/ssp245_projection.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>
