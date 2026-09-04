### 1. Introduction
Albedo is defined as the fraction of incident solar radiation that is reflected by a surface in the shortwave radiation spectrum (Luo et al, 2005). Multi-decadal research in the field of optical remote sensing has formulated and put forth developments to facilitate the retrieval of albedo across different resolutions and space-borne satellites. The majority of natural earth surfaces are anistropical which is generally defined as the reflection of a given surface being directionally dependent while isotropy assumes a directionally independent reflection (Filip et al., 2015). For climate studies and environmental modeling contexts, the absolute accuracy required has been estimated to be between 0.02 - 0.05 (Sellers et al, 1995, Henderson-Sellers and Wilson, 1983, Cihlar et al, 1997). Quantifying surface albedo from space-borne satellite observations is highly dependent on sufficient angular sampling and diversity in order to produce temporally consistent measurements. The bidirectional reflectance distribution function (BRDF) describes the reflectance's dependence on an incident and view angle and BRDFs have been widely used to contextualize anistropical behavior (Lucht et al, 2000). One such BRDF model is the Ross-Thick-Li-Sparse Reciprocal (RTLSR) model which is categorised as a 'kernel-driven BRDF' model, and it has been integrated in the Moderate Resolution Imaging Spectroradiometer (MODIS) product as a result of its ability to describe the surface anisotropy (Zhang et al, 2018). In the design of such kernel-driven BRDF models, the anisotropic behaviors of geometric and volumetric scattering are acquired by kernels and scaled by dynamic weights (Wanner et al., 1999). In the case of white sky albedo (WSA) where diffuse illumination is assumed, the same dynamic weights are used in combination with constants that contextualize the simulated environment of a hemisphere emitting diffuse radiation. In the RTLSR model, this is expressed as the joint sum of the isotropic, geometric and volumetric parameters.

White sky albedo can be calculated by first deriving the black sky albedo from:

$$\\text{bsa}(\\theta_i) = \\int_{0}^{2\\pi} \\int_{0}^{\\pi/2} \\rho(\\theta_i, \\phi_i, \\theta_v, \\phi_v) \\cos(\\theta_v) \\sin(\\theta_v) , d\\theta_v , d\\phi_v$$

Where $$\\rho$$ accounts for the BRDF and $$\\cos(\\theta_v) \\sin(\\theta_v) , d\\theta_v , d\\phi_v$$ represents the projected solid angle which can be simplified into $d\Omega$ (Nicodemus et al, 1977).

$$\\text{bsa}(\\theta_i) = \\int_{0}^{2\\pi} \\int_{0}^{\\pi/2} \\rho(\\theta_i, \\phi_i, \\theta_v, \\phi_v) d\Omega_{projected} $$

In turn, the WSA is derived from:

$$\\text{wsa} = 2 \\int_{0}^{\\pi/2} \\text{bsa}(\\theta_i) \\sin(\\theta_i) \\cos(\\theta_i) , d\\theta_i$$

Where the azimuthal integral is omitted because the theoretical athmospheric conditions in which WSA exists are azimuthally symmetric as previously mentioned. Regarding the field of optical remote sensing, it differentiates between passive and active means, where passive remote sensing implies inference from an external source like the sun, whereas active remote sensing techniques as seen in Synthetic Aperture Radar (SAR) and Light Detection And Ranging (LiDAR) are able to operate independently of the external source (Verhoef, 1998). 


### 2. Materials

#### 2.1. GEDI-derived canopy metrics





Producing albedo measurements for a time series analysis of 24 years poses a specific challenge concerning orbital drift and sensor bias. The MODIS product which belongs to the Terra and Aqua satellites launched in 1999 and 2002, has been used frequently as a common approach to studies involving the quantification of albedo, however, recent evaluations (Feng et al., 2024) have suggested that while the influence of orbital drift is small, it could be biased in the context of a time series analysis. Cross validation was done using the VIIRS product (VNP43MA3) which was designed to be the successor of the MODIS product that was first launched in 2011 aboard of the NPP Suomi satellite. As opposed to MODIS MCD43A3 which has a resolution of 500 meters, the VNP43MA3 product has a native resolution of 1km which is reprojected to 500m in order to match MODIS. The bidirectional reflectance distribution function (BRDF) serves as a main mechanism in conceptualizing the behavior of anisotropic reflectance in relation to the viewing angle. Anisotropy is generally defined as the reflection of a given surface being directionally dependent while isotropy assumes a directionally independent reflection (Filip et al., 2015). Such properties play prominent roles in the design of kernel-driven BRDF models where the anisotropic behaviors of geometric and volumetric scattering are acquired by kernels and scaled by dynamic weights as seen in the Ross-Li model (Wanner et al., 1999). In the case of white sky albedo (WSA) where diffuse illumination is assumed, the same dynamic weights are used in combination with constants that contextualize the simulated environment of a hemisphere emitting diffuse radiation. This is expressed as the joint sum of the isotropic, geometric and volumetric parameters.

$$\\text{wsa} = f_{iso} + (0.189184 \cdot f_{vol}) + (-1.377622 \cdot f_{geo})$$

Where the $$f_{\text{iso}}$$ parameter characterizes the isotropic scattering behavior of the directionally independent surface while $$f_{\text{vol}}$$ describes the anisotropic scattering behavior in relation to canopy density by appropriately scaling its $$K_{\text{vol}}$$ kernel. Lastly, $$f_{\text{geo}}$$ quantifies the geometric-optical scattering by scaling the $$K_{\text{geo}}$$ kernel in accordance to a given surface's three-dimensional structural makeup. When discussing BRDF models in remote sensing, they are generally described as being either empirical or semi-empirical (Jiang & Li, 2008). Empirical models rely on a mathematical curve-fitting approach that does not describe the physical interaction of radiation with a given surface, while semi-empirical models make use of more simplified physical assumptions, allowing them to achieve greater generalization across different settings while retaining computational stability which can be seen in the LiSparse-Dense BRDF model (Li & Strahler, 1992). Both the MCD43 and VNP43 products makes use of the semi-empirical kernel-driven Ross-Li model where the $$K_{\text{vol}}$$ kernel is derived from:

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
Natural earth surfaces generally scatter radiation anisotropically, which can be captured and exploited through multi-angular observations from different view angles, taking into account the position of the sun (Cui et al, 2024). The anisotropical profile of a land surface exhibits different patterns based on the geophysical makeup of a surface, where a 'bell-shape' pattern is common for surfaces that are brighter when observed through smaller view zenith angles (VZA), while a 'bowl-shape' anisotropy describes a surface that is brighter at wider angles (Widlowski et al, 2004). A full BRDF inversion is generally reliant on sufficient and adequately distributed multi-angular observations which are difficult to achieve over shorter periods of time, warranting the use of a magnitude inversion which is described as a backup algorithm that is typical for scenarios with insufficient angular diversity or insufficient confidence with the full inversion as a result of environmental factors such as cloud cover, cloud shadows and other factors that do not allow for high enough confidence (Jin et al., 2003). Magnitude inversions derive their input from priori knowledge data which describe the typical anistropical profile of a given land cover's type (Schaaf et al., 2002). This idea has been extensively described in (Strugnell & Lucht, 2001), where an archetypical BRDF is defined as a representative of a family of BRDFs associated with a land cover type, through which the families derived from a BRDF are generated by applying a multiplicative factor rather than applying the archetypical BRDFs to every pixel, yielding better albedo measurements. To properly examine angular sampling and diversity with a constellation approach, 5 distinct tiles with varying longitudes are selected with all instruments being constrained to observations without cloud cover, cloud shadow and cirrus clouds.

<img width="1589" height="1047" alt="afbeelding" src="https://github.com/user-attachments/assets/fc65c5fc-0a5a-4e39-9e36-bda7b6204037" />


**Figure 2**. Angular density and sampling profiles within tiles h20v11, h18v07, h11v03, h11v08 and h22v15.

| Tile | Valid Obsv. | VZA <30° | VZA 30°-60° | VZA 60°-90° | Principal Plane | Cross principal | Off plane |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **h20v11** | 895 | 496 (55.4%) | 324 (36.2%) | 75 (8.4%) | 344 (38.4%) | 36 (4.0%) |  424 (47.4%) |
| **h18v07** | 1310 | 713 (54.4%) | 427 (32.6%) | 170 (13.0%) | 543 (41.5%) | 10 (0.8%) | 537 (41.0%) |
| **h11v03** | 909 | 558 (61.4%) | 312 (34.3%) |  39 (4.3%) | 358 (39.4%) | 47 (5.2%) | 456 (50.2%) |
| **h11v08** | 654 | 384 (58.7%) | 209 (32.0%) |  61 (9.3%) | 283 (43.3%) | 4 (0.6%) |  266 (40.7%) |
| **h22v15** | 616 | 400 (64.9%) | 159 (25.8%) | 57 (9.3%) | 232 (37.7%) | 29 (4.7%) |  337 (54.7%) |

##### 2.2.3 Weighting multi-angular observations to RTLSR kernels
To retrieve and weight the kernels, Non Negative Least Squares (NNLS) is used in order to constrain the volumetric and geometric weights to positive values. A diagonal weighting matrix of $w_i$ is used for observation $i$. $w_i$ by itself is derived from $w_{\text{SZA}}$, $w_t$ and $w_d$, representing the Solar zenith angle of observation $i$, the temporal weight to observations closest to the median of a given window and the angular component to prioritize unique angles and promote angular diversity. $w_{\text{SZA}}$ comes from:

$$w_{\text{SZA}, i} = n \cdot \frac{\cos(\theta_{s, i})}{\sum_{k=1}^n \cos(\theta_{s, k})}$$

where $\cos(\theta_{s, i})$ scores the SZA at observation $i$

and where multiplying by $n$ accounts for scaling to give average weights across all observations the value of 1

$w_t$ comes from:

$$w_{\text{t}, i} = \exp\left( -\frac{\vert{}t_i - t_{\text{median}}\vert{}}{\tau} \right)$$

Where $t_{\text{median}}$ represents the center of a given temporal window. 

And where $τ$ is the decay constant which can be adjusted according to the size of the window

The angular weight $w_d$ is formulated by:

$$w_{\text{d}, i} = n \cdot \frac{\sum_{k=1}^n \sqrt{(K_{\text{vol}}^{(i)} - K_{\text{vol}}^{(k)})^2 + (K_{\text{geo}}^{(i)} - K_{\text{geo}}^{(k)})^2}}{\sum_{m=1}^n \sum_{k=1}^n \sqrt{(K_{\text{vol}}^{(m)} - K_{\text{vol}}^{(k)})^2 + (K_{\text{geo}}^{(m)} - K_{\text{geo}}^{(k)})^2}}$$

Where a simple euclidian distance is passed to the 2d kernel space to reward unique viewing geometries

To consolidate the outcome, we use Iteratively Reweighted Least Squares (IRLS) where the BRDF curve is fitted with the most suitable weights by downweighting remaining outliers and repeatedly solving for NNLS. To be able to optimize the weights with this approach, the residual error $e_i$ is derived from:

$$e_i = \left\vert{} y_i - \left( f_{\text{iso}}^{(k)} + f_{\text{vol}}^{(k)} K_{\text{vol}, i} + f_{\text{geo}}^{(k)} K_{\text{geo}, i} \right) \right\vert{}$$

Multiplying all four terms together, $w_i$ becomes:

$$w_i = w_{\text{consolidated}, i} \cdot w_{\text{t}, i} \cdot w_{\text{SZA}, i} \cdot w_{\text{d}, i}$$

### 3. General constellation model


<img width="1377" height="1240" alt="afbeelding" src="https://github.com/user-attachments/assets/129cb022-bc43-42ae-83f4-d40abb3da853" />

**Figure 3**. Modeled reflectance of GEDI-derived canopy height at SZA 60, 45, 30 and 15.
