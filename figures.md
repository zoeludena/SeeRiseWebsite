---
layout: page
title: Figures 📈
permalink: /figures/
---

## Figure 1:

Our first figure is one of our temperature prediction using the pattern scaling (linear) emulator. We can see it does a good job predicting sea level rise. This follows the paper "A Semi-Empirical Approach to Projecting Future Sea-Level Rise" ([Rahmstorf 2007](https://www.pik-potsdam.de/~stefan/Publications/Nature/rahmstorf_science_2007.pdf)).

<iframe src="https://zoeludena.github.io/SeeRiseWebsite/assets/figures/tas_predict_vs_historical.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

## Figure 2:

Our second figure is using the pattern scaling (linear) emulator seen in Figure 1 to predict the different Shared Socioeconomic Pathways (SSPs).

<iframe src="https://zoeludena.github.io/SeeRiseWebsite/assets/figures/tas_preds_ssps.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

## Figure 3: 

Our third figure uses three other emulators. We can see the neural network, gaussian processing model, and random forest model perform slightly different than pattern scaling, but still follow the general expected trend.

<iframe src="https://zoeludena.github.io/SeeRiseWebsite/assets/figures/tas_preds_ssp245_compare_emulators" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

## Figure 4:

Our fourth figure plots the NASA projection and uncertainty window, their [Sea Level projection Tool](https://sealevel.nasa.gov/ipcc-ar6-sea-level-projection-tool?type=global). Seen below are the median see level rise predicted every ten years. The shaded ranges show the 17th-83rd percentile ranges for NASA's prediction. The shaded region is based off of a bunch of models that capture a range of uncertainty.

<iframe src="https://zoeludena.github.io/SeeRiseWebsite/assets/figures/nasa_slr_projection.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

## Figure 5:

Our fifth figure plots the NASA projection for SSP 245 and the emulators. We can see that we are on the lower range of uncertainty for NASA's prediction. The emulator that performs the best appears to be the gaussian process.

<iframe src="https://zoeludena.github.io/SeeRiseWebsite/assets/figures/ssp245_projection.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>
