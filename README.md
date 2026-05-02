# niger-albedo-rainfall-dynamics

# Introduction 🇳🇪
Niger, a landlocked country belonging to the Sahel region of Africa, is characterized by a latitudinal rainfall gradient that transitions from the sudanian zone in the south to the Sahara in the north. The Iullemeden aquifer system acts as the country's primary perennial water source and a large part of the hydrological landscape features vernal pools and ephemeral streams. The country has increasingly become a focal point in research and discussions regarding efforts of reversing desertification. Due to Niger's sensitive climate, quantifying the surface energy partitioning along with it's albedo dynamics is vital for assessing the ecological health of a climate vulnerable nation.

# Area of interest and transect
<img width="1235" height="807" alt="afbeelding" src="https://github.com/user-attachments/assets/47069104-9918-41de-9ae3-2f1754cd7fbb" />
The image above shows the transect which goes along the latitudinal gradient of 13.5° to 19.5°. 

## Timeframe 
This study compares the means of 2000-2004 to 2020-2024.

## Comparative sensor analysis

### 1.1 Method
Albedo, which plays an important role in this study, is expressed as a value between 0 and 1. It is generally defined as a surface's ability to reflect light where in an earth science context lower values are found in deep water, grass and asphalt, while clouds and snow yield high values. In the Nigerien and broader Sahelian context, the way albedo is used can vary depending on the objective. For a study focusing on trends of greening and land cover changes, white sky albedo, also referred to as bi-hemispherical reflectance is used due to it making the source of incoming light diffuse as opposed to black sky albedo which instead relies on the angle at which incoming light will hit a surface.

White sky albedo can be calculated by first calculating the black sky albedo:

$$\\text{bsa}(\\theta_i) = \\int_{0}^{2\\pi} \\int_{0}^{\\pi/2} \\rho(\\theta_i, \\phi_i, \\theta_v, \\phi_v) \\cos(\\theta_v) \\sin(\\theta_v) , d\\theta_v , d\\phi_v$$

Where $$\\rho$$ accounts for the viewing and incident solar zenith and azimuth angles respectively.

$$\\text{wsa} = 2 \\int_{0}^{\\pi/2} \\text{bsa}(\\theta_i) \\sin(\\theta_i) \\cos(\\theta_i) , d\\theta_i$$

Additionally, the use of blue sky albedo ($$\\text{A})$$ is a common approach used in climate modeling and the measuring of the surface energy balance. This is attributed to the fact that it accounts for the real world athmospheric conditions of the earth as opposed to bi-hemispherical reflectance and directional-hemispherical reflectance. It can be calculated like:

$$A = (1 - kd) \\text{bsa} + kd , \\text{wsa}$$

Where $$kd$$ represents the diffuse fraction that differentiates between direct sunlight and diffuse light. In the context of the Sahel, $$kd$$ is frequently used to account for Aerosol Optical Depth

### 1.2 Sensor consistency and Cross-Validation Analysis
Producing albedo measurements for a time series analysis of 24 years poses a specific challenge concerning orbital drift and sensor bias. The MODIS product has been used frequently as a common approach to studies involving the quantification of albedo, however, recent evaluations (Feng et al., 2024) have suggested that while the influence of orbital drift is small, it could be biased in the context of a time series analysis. Cross validation was done using the VIIRS product (VNP43IA1) which was designed to be the successor of the MODIS product. As opposed to MODIS which has a resolution of 500 meters, VIIRS has a resolution of 375 meters. A T-test of both sensors points to a significant discrepancy between both MODIS and VIIRS with MODIS as the baseline for the first epoch. While MODIS shows a statistically significant number in relation to it's baseline (4.08e-08), VIIRS shows a much lower significance (8.00e-02). This lower statistical significance could potentially be attributed to it's shorter observational baseline as opposed to MODIS.

### 1.3 External validation
The significant discrepancy between MODIS and VIIRS albedo values justifies the use of external metrics in order to reach a result that is physically consistent. The most noticeable difference along the transect between both results seems to be around the Irhazer shale (16.8 - 18.2°N).
<img width="1496" height="673" alt="VIIRS-albedo" src="https://github.com/user-attachments/assets/065c8401-5ff8-4683-ba24-696d7d7943af" />
_Figure 1.1 (VIIRS) shows that the albedo values seem to converge in the irhazen group_

Another difference that can be observed in figure 1.1 is that the albedo value of the second epoch increases in the far north. External metrics will thus need to validate or challenge this significant increase. These specific trends in figure 1.1 are not present in the graph where MODIS is used for the second epoch. Instead, it shows a more consistent profile.
<img width="1496" height="673" alt="MODIS-albedo" src="https://github.com/user-attachments/assets/9526a4d8-37f4-4d4c-9ea9-dede7ec33196" />
_Figure 1.2 (MODIS) shows that the second epoch (2020-2024) is consistently below it's baseline_

