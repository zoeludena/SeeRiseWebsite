---
layout: home
title: SeeRise
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
            GitHub/Code
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
        Research Paper
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
4. We used a CNN-LTSM emulator, Neural networks excel at climate prediction due to their ability to model complex, non-linear relationships between atmospheric variables. Their deep architectures enable them to learn patterns from large-scale climate data, capturing intricate dependencies that traditional models may overlook. Their adaptability also allows them to generalize well across different climate scenarios, making them valuable for long-term forecasting and extreme weather prediction.

### Sea Level Rise Projection

Using the model described by Rahmstorf (2007), we then produce a linear fit for change in sea level height, regressed on temperature anomaly (temperature difference from a baseline). We take our surface air temperature variable from each of the emulator output files and then use it to train the model on predicted sea level rise in the NOR-ESM2 model for each SSP scenario.

Mathematically, the model equation is of the form:

$$
\frac{dH}{dt} = a(T - T_0)
$$

where  $\frac{dH}{dt}$ is change in sea level height per year, $a$ is a proportionality constant, and $T - T_0$ is temperature relative to a baseline. Finally, to get the total sea level rise, we integrate the rate of sea level rise $\frac{dH}{dt}$ to obtain the total height at the final year of recorded temperature:

$$
H(t) = \int_{t_0}^{t} \frac{dH}{dt} dt.
$$

Finally, as a simple sanity check, we compare visually and quantitatively the predicted sea level rise against both historical satellite data and other projections of sea level rise (NASA).

<iframe src="https://zoeludena.github.io/SeeRiseWebsite/assets/figures/ssp245_projection.html" width="100%" style="aspect-ratio: 4 / 3; border: 0;"></iframe>

## Results

We see rise.

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
