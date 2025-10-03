---
title: "D. Nutrition"
layout: default
parent: FeliX
nav_order: D
math: katex
description: the nutrition section of felix
---

# D. Nutrition
The Nutrition Module focuses on calculating caloric and nutritional availability. It serves two main purposes: linking nutrition to life expectancy, and providing health indicators and key baseline indicators for food system efficiency (e.g. Freshwater Withdrawal per unit of Protein).

## D.1 Caloric and Nutritional Availability
Availability refers to the amount of food content available for human consumption after losses in the supply chain, but before accounting for food waste at the consumer level. While this does not represent actual intake, availability is commonly used for health-related metrics (such as *Prevalence of Undernourishment*) because it is more readily available than direct intake data.

### Caloric Availability
The caloric value is calculated using FAOSTAT (2025a) data on food supply in calories, divided by production in tonnes, and then reaggregated into the eight FeliX food categories.

For total caloric availability:

$$
Cal\_Avail(t) = \sum_{Food} Supply_{Food}(t) \times Cal\_Value_{Food} \quad \text{(Eq. D.1)}
$$ 

For each Age-Sex subgroup:

$$
Cal\_Avail_{Age,Sex}(t) = Cal\_Avail(t) \times Cal\_Distribution_{Age,Sex} \quad \text{(Eq. D.2)}
$$ 

where:

- $Food$ indexes food items,
- $Age, Sex$ index age and sex groups,
- $Cal\_Distribution_{Age,Sex}$ is the share of calories allocated to group $(Age,Sex)$ (assumed constant, based on a reference from 2000–2015).

### Nutritional Availability
The nutritional availability considered includes fat and protein. Nutritional values are calculated using FAOSTAT (2025a) data on protein and fat availability, divided by total food availability in calories, and then reaggregated into the eight FeliX food categories.

For each Nutrient and Food:

$$
Nutr\_Avail_{Food,Nutr}(t)= Supply_{Food}(t) \times Nutr\_Value_{Food,Nutr} \quad \text{(Eq. D.3)}
$$

Total availability of each Nutrient:

$$
Nutr\_Avail_{Nutr}(t) = \sum_{Food} Nutr\_Avail_{Food,Nutr}(t)  \quad \text{(Eq. D.4)} 
$$

For each Age-Sex subgroup:

$$
Nutr\_Avail_{Nutr,Age,Sex}(t) = Nutr\_Avail_{Nutr}(t)  \times Cal\_Distribution_{Age,Sex} \quad \text{(Eq. D.5)}
$$

where $Nutr$ indexes nutrients i.e. protein and fat.


## D.2 Prevalence of Undernutrition (PoU)
This corresponds to SDG Indicator 2.1.1. The Prevalence of Undernourishment (PoU) measures the proportion of a population whose caloric availability falls below the Minimum Dietary Energy Requirement (MDER). This approach follows the FAO methodology (Naiken, 2003) and is calibrated using FAOSTAT (2025b) data.

### Log-Normal Distribution of Caloric Availability

For each age–sex subgroup, caloric availability is modeled using a lognormal distribution. The updated FAO (2014) approach, which incorporates skewness, is not applied in this global version. The ability to capture distributional symmetry is more relevant at national or regional scales than at the aggregated global level.

$$
\ln(Cal\_Avail_{Age,Sex}(t)) \sim \mathcal{N}(\mu, \sigma^2) \quad \text{(Eq. D.6)}
$$

where:

- $\mu = \ln(DES_{Age,Sex}) - \frac{\sigma^2}{2}$  
- $\sigma = 0.3$ (average variability based on FAOSTAT from 200)

### Minimum Dietary Energy Requirement (MDER)
Human energy requirements for an individual in a given sex/age class are determined on the basis of normative requirements for basic metabolic rate (BMR) per kilogram of body mass, multiplied by the ideal weights that a healthy person of that sex/age class may have, given his or her height, and then multiplied by a coefficient of physical activity level (PAL) to take into account physical activity. 

Specific formulas for basal metabolic rate (BMR) are provided in the Human Energy Requirements report (FAO, 2008). BMR estimates rely on BMI reference values from WHO guidelines combined with average heights from WHO growth standards (WHO, 2025). 

$$
MDER_{Age,Sex} = BMR_{Age,Sex} \times PAL_{Age,Sex}\quad \text{(Eq. D.7)}
$$

where:

- $BMR_{Age,Sex}$ = basal metabolic rate for the subgroup (kcal/day), depending on age, sex, and body weight.  
- $PAL_{Age,Sex}$ = physical activity level, reflecting typical energy expenditure. Here we assume $PAL = 1.5$ based on UN guidelines.  

### PoU Calculation

The PoU for each subgroup is the probability that DES is below MDER. The total PoU for the population is obtained by aggregating across all subgroups, weighted by population size.


$$
PoU_{Age,Sex}(t) = P(Cal\_Avail_{Age,Sex}(t) < MDER_{Age,Sex}) 
= \Phi\left(\frac{\ln(MDER_{Age,Sex}) - \mu}{\sigma}\right)\quad \text{(Eq. D.8)}
$$

$$
PoU_{Total}(t) = \sum_{Age,Sex} PoU_{Age,Sex}(t) \cdot Population_{Age,Sex}(t)\quad \text{(Eq. D.9)}
$$

where $\Phi$ is the standard normal cumulative distribution function (CDF).  


## References

- FAOSTAT, 2025a. FAOSTAT Food Balance Sheets. [https://www.fao.org/faostat/en/#data/FBS](https://www.fao.org/faostat/en/#data/FBS)  
- FAOSTAT, 2025b. FAOSTAT Suite of Food Security Indicators. [https://www.fao.org/faostat/en/#data/FS](https://www.fao.org/faostat/en/#data/FS)  
- Food and Agriculture Organization of the United Nations, 2014. Revision of the methodology for the estimation of the prevalence of undernourishment: Asia and Pacific Commission on Agricultural Statistics. FAO. [https://www.fao.org/fileadmin/templates/ess/documents/apcas25/APCAS-14-8.2-PoU-Method.pdf](https://www.fao.org/fileadmin/templates/ess/documents/apcas25/APCAS-14-8.2-PoU-Method.pdf)  
- Food and Agriculture Organization of the United Nations, Statistics Division, 2008. FAO methodology for the measurement of food deprivation: Updating the minimum dietary energy requirements. FAO. [https://www.fao.org/fileadmin/templates/ess/documents/food_security_statistics/metadata/undernourishment_methodology.pdf](https://www.fao.org/fileadmin/templates/ess/documents/food_security_statistics/metadata/undernourishment_methodology.pdf)  
- Naiken, L., 2003. Keynote paper: FAO methodology for estimating the prevalence of undernourishment. In *Measurement and assessment of food deprivation and undernutrition. Proceedings of the International Scientific Symposium convened by the Agriculture and Economic Development Analysis Division in Rome, 26–28 June 2002.* FAO. [https://www.fao.org/4/y4249e/y4249e06.htm](https://www.fao.org/4/y4249e/y4249e06.htm)  
- World Health Organization, 2025. Length/height-for-age — WHO Child Growth Standards. [https://www.who.int/tools/child-growth-standards/standards/length-height-for-age](https://www.who.int/tools/child-growth-standards/standards/length-height-for-age)  

