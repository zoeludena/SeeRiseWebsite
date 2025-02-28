---
layout: home
title: SeeRise 🌊
---

# Visualizing Emulated Sea Level Rise on Coastal Regions

<div style="display: flex; gap: 10px; align-items: center;">
    <a href="https://github.com/zoeludena/SeeRise" target="_blank">
        <button style="background-color: #6C7A89; color: white; border: none; padding: 10px 20px; 
                    border-radius: 8px; font-size: 16px; cursor: pointer; transition: 0.3s; 
                    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);"
                onmouseover="this.style.backgroundColor='#5A6978'; this.style.transform='scale(1.05)';" 
                onmouseout="this.style.backgroundColor='#6C7A89'; this.style.transform='scale(1)';"
                onmousedown="this.style.backgroundColor='#485563'; this.style.transform='scale(0.95)';"
                onmouseup="this.style.backgroundColor='#5A6978'; this.style.transform='scale(1.05)';">
            💽GitHub/Code
        </button>
    </a>

<a href="https://github.com/zoeludena/SeeRiseWebsite/blob/main/assets/SeeRise_Paper.pdf" target="_blank">
    <button style="background-color: #3498db; color: white; border: none; padding: 10px 20px; 
                border-radius: 8px; font-size: 16px; cursor: pointer; transition: 0.3s; 
                box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);"
            onmouseover="this.style.backgroundColor='#2980b9'; this.style.transform='scale(1.05)';" 
            onmouseout="this.style.backgroundColor='#3498db'; this.style.transform='scale(1)';"
            onmousedown="this.style.backgroundColor='#1f669a'; this.style.transform='scale(0.95)';"
            onmouseup="this.style.backgroundColor='#2980b9'; this.style.transform='scale(1.05)';">
        📃Research Paper
    </button>
</a>
</div>

<p><br></p>

## Our Inspiration

The advent of sea level rise can have devastating consequences on coastal areas all around the world.  Low-lying regions—such as Florida, a state particularly susceptible to sea level rise due to its low-lying topography and extensive coastline—are especially a major focal point when it comes to modeling sea level rise as they are most vulnerable to changes. Using the method described by "A Semi-Empirical Approach to Projecting Future Sea-Level Rise" ([Rahmstorf 2007](https://www.pik-potsdam.de/~stefan/Publications/Nature/rahmstorf_science_2007.pdf)), which regresses the rate of sea level rise on surface air temperature anomaly, our team coupled this model with emulators from the “ClimateBench v1.0: A Benchmark for Data-Driven Climate Projections” ([Watson-Parris et al. 2022](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2021MS002954)) to create a predictor capable of simulating sea level rise in any future emission scenario, not just the ones prescribed by SSPs. This impact is then visualized using high-resolution topography data to assess the potential transformation of Florida’s coastal landscape, which can aid policymakers in developing mitigation and adaptation strategies.

## Methods

### Climate Model Emulators

Our first objective was to tune the hyperparameter for each emulator model. The emulators are fitted to historical data and each SSP, excluding SSP 245 which is used for validation. The emulators take in any combination of greenhouse gas emissions as input, but in order to assure ourselves that the outputs are sensible, we used the prescribed emissions for the SSP scenarios for training and validation. The emulators are used to predict surface air temperature based on difference emission inputs, and we later use the predicted temperature as the input to our sea level model.

We used four different emulators based on what we learned in the ClimateBench and our previous research, [ResearchOnClimate](https://github.com/zoeludena/ResearchOnClimate/blob/main/Utilizing_Emulators_to_Explore_the_Climate_Model_Parameter_Space.pdf):

1. We used a Pattern Scaling emulator. In the Rahmstorf paper they use linear regression trained on historical temperature and the difference between the predicted temperature and the average. This makes our pattern scaling emulator a fantastic one-to-one comparison.
2. We used a Gaussian Process emulator. Climate systems are governed by complex, smooth, and highly nonlinear relationships, making Gaussian Process (GP) emulators well-suited for predicting future climate scenarios. Building on our previous research, we chose to utilize the original GP model from ClimateBench as a foundation for our work. This approach leverages the flexibility and uncertainty quantification capabilities of GPs to improve climate predictions.
3. We used a Random Forest emulator. While decision trees capture non-linear relationships well, they tend to overfit. Random Forest mitigates this by averaging predictions, reducing variance, and enhancing robustness. This makes it ideal for climate model emulation, where multiple target variables require separate models.
4. We used a CNN-LTSM emulator. Neural networks excel at climate prediction due to their ability to model complex, non-linear relationships between atmospheric variables. Their deep architectures enable them to learn patterns from large-scale climate data, capturing intricate dependencies that traditional models may overlook. Their adaptability also allows them to generalize well across different climate scenarios, making them valuable for long-term forecasting and extreme weather prediction.

### Sea Level Rise Projection

Using the model described by Rahmstorf (2007), we then produce a linear fit for change in sea level height, regressed on temperature anomaly (temperature difference from a baseline). We take our surface air temperature variable from each of the emulator output files and then use it to train the model on predicted sea level rise in the NOR-ESM2 model for each SSP scenario.

Mathematically, the model equation is of the form:

$$
\frac{dH}{dt} = a(T - T_0)
$$

where  $\frac{dH}{dt}$ is change in sea level height per year, \\(a\\) is a proportionality constant, and \\(T - T_0\\) is temperature relative to a baseline. Finally, to get the total sea level rise, we integrate the rate of sea level rise \\(\frac{dH}{dt}\\) to obtain the total height at the final year of recorded temperature:

$$
H(t) = \int_{t_0}^{t} \frac{dH}{dt} dt.
$$

Finally, as a simple sanity check, we compare visually and quantitatively the predicted sea level rise against both historical satellite data and other projections of sea level rise (NASA).

**Comparing Projections of Sea Level Rise with Historical**

<iframe src="https://zoeludena.github.io/SeeRiseWebsite/assets/figures/tas_predict_vs_historical.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

**Comparing Projections of Sea Level Rise from NASA**

<iframe src="https://zoeludena.github.io/SeeRiseWebsite/assets/figures/ssp245_emulator_preds.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

## Results

### Florida Sea Level Rise

Florida is a state particularly susceptible to sea level rise due to its low-lying topography and extensive coastline. To visualize the rise in sea level, we used digital elevation models (DEM). DEMs are a representation of the bare ground topographic surface of the Earth excluding trees, buildings, and any other surface objects. They are computed via LiDAR data (which is essentially a 3D scan of the Earth's surface), algorithms, and other data sources are used to construct the true elevation of just the land alone.

We chose the following locations:
 - Sanibel Island
 - Fort Myers Beach
 - Courtenay

We then took the median amount of sea level rise and determined how much land would be submerged. For this paper we used the cumulative amount of carbon dioxide in 2100 for SSP 245, which is about 4520 Gigatons of carbon dioxide.

You can visualize these changes on our [application](https://zoeludena.github.io/SeeRiseWebsite/app/) or [figures](https://zoeludena.github.io/SeeRiseWebsite/figures/).

### Expected Sea Level Rise

According to [NASA projections](https://sealevel.nasa.gov/ipcc-ar6-sea-level-projection-tool?type=global), the expected cumulative rise in sea level between 2015-2100 would be 536.4 mm. We found this data from NASA's Sea Level Projection tool, modified for our year range (2015-2100).

NASA includes sea level rise starting from 2011, which is why their number on the website (556 mm) is different than ours.

### Predicted Sea Level Rise

Our predictions were calculated by keeping the methane, sulfur dioxide, and black carbon at 2025's values for SSP 245. We then linearly increased the carbon dioxide from 2015 to 2100, where it ended at 4520 Gigatons of carbon dioxide.

In the Rahmstorf paper they use linear regression trained on historical temperature and the difference between the predicted temperature and the average. This makes our pattern scaling emulator a fantastic one-to-one comparison when looking at predicted sea level rise. For the pattern scaling to sea level rise pipeline, it is then thought of as using cumulative carbon dioxide to compute air surface temperature (TAS), which is then used to calculate the rate of sea level rise.

**Prediction Error Comparison**

| Emulator         | Predicted (mm) | 536.4 - Predicted (mm) |
|-----------------|---------------|------------------------|
| Pattern Scaling | 513.6         | 22.8                   |
| Gaussian Process | 511.6         | 24.8                   |
| Random Forest   | 511.3         | 25.1                   |
| CNN-LSTM        | 417.0         | 119.4                  |

**Comparing Emulators with NASA Keeping Greenhouse Gases Fixed at 2025**

<iframe src="https://zoeludena.github.io/SeeRiseWebsite/assets/figures/2025_fixed_emulator_preds.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

### Validation Set Sea Level Rise Analysis

As we can see, the Pattern Scaling, Gaussian Process, and Random Forest emulators perform about equally well. They are under predicting by the size of a peanut (20 mm) or about an inch (25 mm).

The CNN-LTSM model performs the worst. The measurement is off by about a standard playing card's length (120 mm).

This under prediction is caused because we decided to keep the other greenhouse gases constant. The values are from SSP245 at the year 2025. If we scaled our other greenhouse gases input appropriately, the emulators would give more accurate TAS values which in turn would lead to greater performance for our sea level rise regression.

<script type="text/javascript" async 
  src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script type="text/javascript" async 
  id="MathJax-script" 
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>
<script>
  window.MathJax = {
    tex: {
      inlineMath: [['$', '$'], ['\\(', '\\)']],
      displayMath: [['$$', '$$'], ['\\[', '\\]']]
    },
    svg: {
      fontCache: 'global'
    }
  };
</script>
