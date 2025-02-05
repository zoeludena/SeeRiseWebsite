---
layout: home
title: SeeRise
---

# Visualizing Emulated Sea Level Rise on Coastal Regions

<a href="https://github.com/zoeludena/SeeRise" target="_blank">
    <button style="background-color: #007BFF; color: white; border: none; padding: 10px 20px; 
               border-radius: 8px; font-size: 16px; cursor: pointer; transition: 0.3s; 
               box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);"
                onmouseover="this.style.backgroundColor='#0056b3'; this.style.transform='scale(1.05)';" 
                onmouseout="this.style.backgroundColor='#007BFF'; this.style.transform='scale(1)';"
                onmousedown="this.style.backgroundColor='#003f7f'; this.style.transform='scale(0.95)';"
                onmouseup="this.style.backgroundColor='#0056b3'; this.style.transform='scale(1.05)';">
            GitHub Page</button>
</a>

## Introduction

Where will become the next Atlantis? It is no suprise that with climate change the sea levels are rising. We are curious as to how much they will rise and where. Low coastal areas are in danger with sea level rise.

## Methods

To predict the future, we built upon our previous research paper (TODO), that used emulators in an effort to predict the world's climate (temperature, precipitation, ...). From there we used the (TODO) paper's findings to re-create predicting sea level rise.

## Results

We see rise.

Our first figure is one of our temperature prediction using the pattern scaling (linear) emulator. We can see it does a good job predicting sea level rise. This follows the paper (TODO).

<iframe src="assets/figures/tas_predict_vs_historical.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

Our second figure is using the pattern scaling (linear) emulator to predict the different Shared Socioeconomic Pathways (SSPs).

<iframe src="assets/figures/tas_preds_ssps.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

Our third figure uses three other emulators. We can see the neural network, gaussian processing model, and random forest model perform slightly different than pattern scaling, but still follow the general expected trend.

<iframe src="assets/figures/tas_preds_ssp245_compare_emulators" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

Our fourth figure plots the NASA projection and uncertainty window. This is from (TODO).

<iframe src="assets/figures/nasa_slr_projection.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

Our fifth figure plots the NASA projection for SSP 245 and the emulators. We can see that we are underpredicting quite a bit. The emulator that performs the best appears to be the gaussian process.

<iframe src="assets/figures/ssp245_projection.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>
