# niger-albedo-rainfall-dynamics

# Introduction 
Niger, a landlocked country belonging to the Sahel region of Africa, is characterized by a latitudinal rainfall gradient that transitions from the sudanian zone in the south to the Sahara in the north. The Iullemeden aquifer system acts as the country's primary perennial water source and a large part of the hydrological landscape features vernal pools and ephemeral streams. The country has increasingly become a focal point in research and discussions regarding efforts of reversing desertification. Due to Niger's sensitive climate, quantifying the surface energy partitioning along with it's albedo dynamics is vital for assessing the ecological health of a climate vulnerable nation.

# Area of interest and transect
The image above shows the transect which goes along the latitudinal gradient of 13.5° to 19.5°. 

## Timeframe 
This study compares the means of 2000-2004 to 2020-2024.

## Comparative sensor analysis

### 1. Introduction
Albedo, which plays an important role in this study, is expressed as a value between 0 and 1. It is generally defined as a surface's ability to reflect light where in an earth science context lower values are found in deep water, grass and asphalt, while clouds and snow yield high values. In the Nigerien and broader Sahelian context, the way albedo is used can vary depending on the objective. For a study focusing on trends of greening and land cover changes, white sky albedo, also referred to as bi-hemispherical reflectance is often used due to it making the source of incoming light diffuse as opposed to black sky albedo which instead relies on the angle at which incoming light will hit a surface.

White sky albedo can be calculated by first calculating the black sky albedo:

$$\\text{bsa}(\\theta_i) = \\int_{0}^{2\\pi} \\int_{0}^{\\pi/2} \\rho(\\theta_i, \\phi_i, \\theta_v, \\phi_v) \\cos(\\theta_v) \\sin(\\theta_v) , d\\theta_v , d\\phi_v$$

Where $$\\rho$$ accounts for the viewing and incident solar zenith and azimuth angles respectively.

$$\\text{wsa} = 2 \\int_{0}^{\\pi/2} \\text{bsa}(\\theta_i) \\sin(\\theta_i) \\cos(\\theta_i) , d\\theta_i$$

Additionally, the use of blue sky albedo ($$\\text{A})$$ is a common approach used in climate modeling and the measuring of the surface energy balance. This is attributed to the fact that it accounts for the real world athmospheric conditions of the earth as opposed to bi-hemispherical reflectance and directional-hemispherical reflectance. It can be calculated like:

$$A = (1 - kd) \\text{bsa} + kd , \\text{wsa}$$

Where $$kd$$ represents the diffuse fraction that differentiates between direct sunlight and diffuse light. In the context of the Sahel, $$kd$$ is frequently used to account for Aerosol Optical Depth. 

### 2. Sensor consistency and Cross-Validation Analysis
Producing albedo measurements for a time series analysis of 24 years poses a specific challenge concerning orbital drift and sensor bias. The MODIS product which belongs to the Terra and Aqua satellites launched in 1999 and 2002, has been used frequently as a common approach to studies involving the quantification of albedo, however, recent evaluations (Feng et al., 2024) have suggested that while the influence of orbital drift is small, it could be biased in the context of a time series analysis. Cross validation was done using the VIIRS product (VNP43MA3) which was designed to be the successor of the MODIS product that was first launched in 2011 aboard of the NPP Suomi satellite. As opposed to MODIS MCD43A3 which has a resolution of 500 meters, the VNP43MA3 product has a native resolution of 1km which is reprojected to 500m in order to match MODIS. The bidirectional reflectance distribution function (BRDF) serves as a main mechanism in conceptualizing the behavior of anisotropic reflectance in relation to the viewing angle. Anisotropy is generally defined as the reflection of a given surface being directionally dependent while isotropy assumes a directionally independent reflection (Filip et al., 2015). Such properties play prominent roles in the design of kernel-driven BRDF models where the anisotropic behaviors of geometric and volumetric scattering are acquired by kernels and scaled by dynamic weights as seen in the Ross-Li model (Wanner et al., 1999). In the case of white sky albedo (WSA) where diffuse illumination is assumed, the same dynamic weights are used in combination with constants that contextualize the simulated environment of a hemisphere emitting diffuse radiation. This is expressed as the joint sum of the isotropic, geometric and volumetric parameters.

$$\\text{wsa} = f_{iso} + (0.189184 \cdot f_{vol}) + (-1.377622 \cdot f_{geo})$$

Where the $$f_{\text{iso}}$$ parameter characterizes the isotropic scattering behavior of the directionally independent surface while $$f_{\text{vol}}$$ describes the anisotropic scattering behavior in relation to canopy density by appropriately scaling its $$K_{\text{vol}}$$ kernel. Lastly, $$f_{\text{geo}}$$ quantifies the geometric-optical scattering by scaling the $$K_{\text{geo}}$$ kernel in accordance to a given surface's three-dimensional structural makeup. When discussing BRDF models in remote sensing, they are generally described as being either empirical or semi-empirical (Jiang & Li, 2008). Empirical models generally rely on a mathematical curve-fitting approach that does not describe the physical interaction of radiation with a given surface, while semi-empirical models make use of more simplified physical assumptions, allowing them to achieve greater generalization across different settings while retaining computational stability which can be seen in the LiSparse-Dense BRDF model (Li & Strahler, 1992). Both the MCD43 and VNP43 products makes use of the semi-empirical kernel-driven Ross-Li model where the $$K_{\text{vol}}$$ kernel is derived from:

$$K_{\text{vol}} = \frac{\left(\frac{\pi}{2} - \xi\right) \cos\xi + \sin\xi}{\cos\theta_s + \cos\theta_v} - \frac{\pi}{4}$$

where $$\xi$$ describes the scattering phase angle between the source of radiation (at angle $$\theta_s$$) and the satellite sensor (at angle $$\theta_v$$) coupled with:

$$\cos\xi = \cos\theta_s \cos\theta_v + \sin\theta_s \sin\theta_v \cos\Delta\phi$$

Where $\Delta\phi$ is derived from:

$$\Delta\phi = \phi_s - \phi_v$$

 $$K_{\text{geo}}$$ is gathered from the LiSparse-Reciprocal kernel which is constructed symmetrically and is expressed as:

$$K_{\text{geo}} = \frac{1 + \cos\xi'}{2} \sec\theta'_s \sec\theta'_v - O(\theta'_s, \theta'_v, \Delta\phi)$$

Where $O$ represents the overlap function that is written as:

$$O(\theta'_s, \theta'_v, \Delta\phi) = \frac{1}{\pi} (\gamma - \sin\gamma \cos\gamma) \left(\sec\theta'_s + \sec\theta'_v\right)$$

Where $$\gamma$$ is derived from distance ($$D$$) and overlap ratio ($$R$$) respectively. They are expressed as:

$$D = \sqrt{\tan^2\theta'_s + \tan^2\theta'_v - 2\tan\theta'_s\tan\theta'_v\cos\Delta\phi}$$

$$R = \frac{h}{b}\sqrt{\tan^2\theta'_s + \tan^2\theta'_v - 2\tan\theta'_s\tan\theta'_v\cos\Delta\phi}$$

Where $$R$$ can be simplified into $$R = \frac{h}{b} \cdot D$$

#### 2.2 inter-sensor comparison
Globally, in the context of the retrieval of surface derived indices, VIIRS has been described as achieving results sufficient to be considered a suitable successor to the MODIS product (Han et al, 2025, Liu et al, 2017). Its configurations are similar to that of MODIS, having a spectral range of $0.4\ \mu\text{m}$ to $12.5\ \mu\text{m}$. As previously mentioned, the MODIS product has been and is currently influenced by orbital drift, impacting Aqua and Terra's designated equatorial-crossing mean local times of 10:30 AM and 13:30 PM. As a result, NASA has performed inclination adjustment maneuvers (IAM) which involve the correction of the orbital inclination of a given instrument's satellite. This change in inclination can be expressed as:

$$\Delta v = 2 v \sin\left(\frac{\Delta i}{2}\right)$$
 
Where $$\Delta i$$ is the targeted adjustment, and $$\Delta v$$ is the velocity vector that is required to perform the burn that will realize the IAM. For both Aqua and Terra, NASA has ceased IAM's, with Terra having received it's last maneuver on Febuary 27, 2020 and Aqua one year later on March 8, 2021. When it comes to the comparison and cross-calibration of satellite missions, a frequently mentioned concept is the usage of pseudo invariant calibration sites (PICS). PICS are characterized by having high temporal stability and possessing high isotropy. Additionally, PICS feature an absence of flora and thus, they are generally situated in desert environments such as the Sahara and Antarctica. The combination of these factors allow for the observation of discrepancies like sensor bias, sensor degradation and orbital drift. As previously mentioned, the MODIS product is influenced by orbital drift which has made Terra and Aqua deviate from their mean local times, causing an overestimation trend. This is also visible in a comparison of results from white sky albedo of the Niger-1 PICS, situated at 9.36° N, 20.41° E.

<img width="1990" height="690" alt="afbeelding" src="https://github.com/user-attachments/assets/c0f39cc8-995d-46a9-bb8a-98ea55aeea16" />

**Figure 1**. For the epoch of 2020-2025, MODIS has an increasingly higher trend as opposed to its previous more stable epoch in the Niger-1 PICS.

##### 2.2.1 Spectral Band Adjustment Factors
Analyses of the comparison and intercalibration of sensors can be exacerbated by inherent differences in their relative spectral responses (RSRs). These differences can be understood and accounted for by using Spectral Band Adjustment Factors (SBAFs) which are derived by convolving hyperspectral data from a given spectral library (Chander et al, 2013). The retrieval of an SBAF depends on a reference sensor and a target sensor where the RSRs are integrated with the observed reflectance of the spectral library, which after the SBAF can be calculated.

$$\bar{\rho}_\lambda = \frac{\int \rho_\lambda \text{RSR}_\lambda \, d\lambda}{\int \text{RSR}_\lambda \, d\lambda}$$

Where $$\bar{\rho}_\lambda$$ is the simulated band reflectance.

And where $$\{\rho}_\lambda$$ is the spectral library's observed reflectance.

$$\text{SBAF} = \frac{\bar{\rho}{\lambda}_{\text{reference}}}{\bar{\rho}{\lambda}_{\text{target}}} = \frac{\frac{\int \rho_\lambda \text{RSR}_{\lambda, \text{reference}} \, d\lambda}{\int \text{RSR}_{\lambda, \text{reference}} \, d\lambda}}{\frac{\int \rho_\lambda \text{RSR}_{\lambda, \text{target}} \, d\lambda}{\int \text{RSR}_{\lambda, \text{target}} \, d\lambda}}$$

In 2016, the NASA Langley Research Center (LaRC) built a SCIAMACHY-based SBAF tool with data obtained from the Envisat program. comparisons between the SCIAMACHY-derived SBAFs were done with those of Hyperion and Global Ozone Monitoring Experiment-2 (GOME-2), where it was shown that the SCIAMACHY-derived SBAFs fell within a small margin (0.1%–0.3%) of SBAFs derived from the mentioned counterparts (Scarino et al. 2016, Bovensmann et al. 1999). Table 1 shows the SBAF values used for intercalibration derived from the LaRC SCIAMACHY-based product.

| MODIS AQUA Ch. | NPP-VIIRS-GT Ch. | SBAF | R^2 | Reference Spectra | Offset | StdErrReg% | StdErrSlp% |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 0.65 micron (Red)  | 0.68 micron (M5)  | 1.082 | 0.999  | 587  |-0.004661  | 0.456  | 1.3116e-01   |
| 0.86 micron (NIR)  | 0.86 micron (M7)  | 1.015 | 0.999  | 587  | -0.002953  | 0.2942  | 8.3280e-02   |
| 0.47 micron (SWIR)  | 0.48 micron (M3)  | 1.007 | 0.9968  | 587  | 0.003755  | 1.032  | 2.3485e-01   |

##### 2.2.2 Angular diversity
Natural earth surfaces generally scatter radiation anisotropically, which can be captured and exploited through multi-angular observations from different view angles, taking into account the position of the sun (Cui et al, 2024). The anisotropical profile of a land surface exhibits different patterns based on the geophysical makeup of a surface, where a 'bell-shape' pattern is common for surfaces that are brighter when observed through smaller view zenith angles (VZA), while a 'bowl-shape' anisotropy describes a surface that is brighter at wider angles (Widlowski et al, 2004). 
