---
title: "8. Nutrition"
layout: default
parent: FeliX
nav_order: 8
math: katex
description: the nutrition section of felix
---

# 8. Nutrition
The Nutrition Module in FeliX focuses on estimating caloric and nutritional availability based on the food produced. It serves two main purposes. First, it links nutritional outcomes to social indicators such as health and well-being, allowing for a better understanding of how food system performance affects human development. Second, it establishes key baseline indicators to assess the efficiency of food systems, for example, measuring freshwater withdrawal per unit of protein. 

## 8.1 Caloric and Nutritional Availability
Availability refers to the amount of food content available for human consumption after losses in the supply chain, but before accounting for food waste at the consumer level. While this does not represent actual intake, availability is commonly used for health-related metrics (such as *Prevalence of Undernourishment*) because it is more readily available than direct intake data.

### Caloric Availability
Caloric Availability captures the total amount of energy available from food (Equation 8.1) and also how they might be distributed based on age-sex subgroup (Equation 8.2). The caloric value ($Cal_Value_{Food}$) used is calculated using FAO (2025a) data on food supply in calories, divided by production in tonnes, and then reaggregated into the eight FeliX food categories. The caloric distribution of availability ($Cal_Distribution_{Age,Sex}$) is assumed to be a constant that follows the same distribution of caloric demand in each group (Age,Sex). Both distributions are estimated based on a reference dataset from 2000-2015.

For total caloric availability:

$$
Cal\_Avail(t) = \sum_{Food} Supply_{Food}(t) \times Cal\_Value_{Food} \quad \text{(Eq. 8.1)}
$$ 

For each Age-Sex subgroup:

$$
Cal\_Avail_{Age,Sex}(t) = Cal\_Avail(t) \times Cal\_Distribution_{Age,Sex} \quad \text{(Eq. 8.2)}
$$ 

where:

- $Food$ indexes food items,
- $Age, Sex$ index age and sex groups,
- $Cal\_Distribution_{Age,Sex}$ is the share of calories allocated to group $(Age,Sex)$ (assumed constant, based on a reference from 2000–2015).

### Nutritional Availability
Nutritional Availability accounts for key macronutrients—i.e. fat and protein—available in the food supply. The model captures total nutrient availability (Equation 8.4), disaggregated by food categories (Equation 8.3) and further by age–sex groups (8.5). Nutritional values ($Nutr\_Value_{Food,Nutr}$) are calculated using FAOSTAT (2025a) data on protein and fat availability, divided by total food availability in calories, and then reaggregated into the eight FeliX food categories. The distribution of nutrients based on age-sex groups follows the caloric distribution ($Cal\_Distribution_{Age,Sex}$).

For each Nutrient and Food:

$$
Nutr\_Avail_{Food,Nutr}(t)= Supply_{Food}(t) \times Nutr\_Value_{Food,Nutr} \quad \text{(Eq. 8.3)}
$$

Total availability of each Nutrient:

$$
Nutr\_Avail_{Nutr}(t) = \sum_{Food} Nutr\_Avail_{Food,Nutr}(t)  \quad \text{(Eq. 8.4)} 
$$

For each Age-Sex subgroup:

$$
Nutr\_Avail_{Nutr,Age,Sex}(t) = Nutr\_Avail_{Nutr}(t)  \times Cal\_Distribution_{Age,Sex} \quad \text{(Eq. 8.5)}
$$

where $Nutr$ indexes nutrients, i.e., protein and fat.

Both Caloric and Nutritional Availabilities are compared with historical data from FAOSTAT (2025a), where caloric and nutritional values are further calibrated (within 15% alignment of historical values) to have a better fit with historical data. The model generally displays a good fit for both availabilities.

## 8.2 Prevalence of Undernutrition (PoU)
Prevalence of Undernourishment (PoU) is the Sustainable Development Goal (SDG) Indicator 2.1.1, used to monitor progress towards ending hunger and ensuring access to safe, nutritious and sufficient food. PoU effectively estimates the proportion of a population whose habitual dietary energy consumption is insufficient to meet the minimum energy requirements for an active and healthy life. 

It is calculated by comparing the distribution of Dietary Energy Supply (DES) with the Minimum Dietary Energy Requirement (MDER). The DES represents the average per capita caloric availability of food, while the MDER defines the lower threshold of adequate intake for each population group. By integrating these two measures, the PoU quantifies the share of individuals whose energy consumption falls below the minimum required level. This approach follows the FAO (2014) methodology and is calibrated using Food Balance Sheet data (FAOSTAT, 2025a).

### Log-Normal Distribution of Dietary Energy Supply

For each age–sex subgroup, the Dietary Energy Supply is modelled using a lognormal distribution (see Equation 8.6). This distribution adequately represents empirical patterns of energy supply across populations. The lognormal form is particularly appropriate as it is bounded by zero, reflecting the realistic condition that no individual within a population cohort can have a negative energy intake. The main parameters of the distribution are the mean ($\mu$), which corresponds to the caloric availability described in the previous section, and the variance ($\sigma^2$), which captures the degree of variability—larger values indicate greater dispersion. 

The formulation applied is the updated approach of FAO (2014), which incorporates a skewness parameter to the original formula by Naiken (2003) for the purpose of capturing distributional (a)symmetries at national or regional scales, such as increasing inequalities within populations. As FeliX is at an aggregated global scale, the baseline assumption is no skew and that any variation of this skew can be explored in scenario experiments or the Regional FeliX.

$$
\ln(DES_{Age,Sex}(t)) \sim \mathcal{N}(\mu, \sigma^2, \alpha) \quad \text{(Eq. 8.6)}
$$

where:

- Mean: $\mu = \ln(Cal\_Avail_{Age,Sex}(t)) - \frac{\sigma^2}{2}$  
- Variance: $\sigma = 0.3$ (average variability based on FAOSTAT (2025a) from 2000-2024)
- Skew: $\alpha = 0$ (baseline assumes no skew)

### Minimum Dietary Energy Requirement (MDER)
Human energy requirements for an individual in a given sex/age class are determined on the basis of normative requirements for basic metabolic rate (BMR) per kilogram of body mass, multiplied by the ideal weights that a healthy person of that sex/age class may have, given his or her height, and then multiplied by a coefficient of physical activity level (PAL) to take into account physical activity. 

Specific formulas for basal metabolic rate (BMR) are provided in the Human Energy Requirements report (FAO, 2008). BMR estimates rely on BMI reference values from WHO guidelines combined with average heights from WHO growth standards (WHO, 2025). 

$$
MDER_{Age,Sex} = BMR_{Age,Sex} \times PAL_{Age,Sex}\quad \text{(Eq. 8.7)}
$$

where:

- $BMR_{Age,Sex}$ = basal metabolic rate for the subgroup (kcal/day), depending on age, sex, and body weight.  
- $PAL_{Age,Sex}$ = physical activity level, reflecting typical energy expenditure. Here we assume $PAL = 1.5$ based on UN guidelines.  

### Prevalence of Undernourishment

The PoU for each subgroup is the probability that DES is below MDER. The total PoU for the population is obtained by aggregating across all subgroups, weighted by population size.


$$
PoU_{Age,Sex}(t) = P(DES_{Age,Sex}(t) < MDER_{Age,Sex}) 
= \Phi\left(\frac{\ln(MDER_{Age,Sex}) - \mu}{\sigma}\right)\quad \text{(Eq. 8.8)}
$$

$$
PoU_{Total}(t) = \sum_{Age,Sex} PoU_{Age,Sex}(t) \cdot Population_{Age,Sex}(t)\quad \text{(Eq. 8.9)}
$$

where $\Phi$ is the standard normal cumulative distribution function (CDF).


## References

- FAO, 2008. Human Energy Requirements: Report of a Joint FAO/WHO/UNU Expert Consultation. Food and Agriculture Organization of the United Nations, Rome.
- FAO, 2014. Revision of the methodology for the estimation of the prevalence of undernourishment: Asia and Pacific Commission on Agricultural Statistics. FAO. [https://www.fao.org/fileadmin/templates/ess/documents/apcas25/APCAS-14-8.2-PoU-Method.pdf](https://www.fao.org/fileadmin/templates/ess/documents/apcas25/APCAS-14-8.2-PoU-Method.pdf)
- FAOSTAT, 2025a. FAOSTAT Food Balance Sheets. [https://www.fao.org/faostat/en/#data/FBS](https://www.fao.org/faostat/en/#data/FBS)  
- Naiken, L., 2003. Keynote paper: FAO methodology for estimating the prevalence of undernourishment. In *Measurement and assessment of food deprivation and undernutrition. Proceedings of the International Scientific Symposium convened by the Agriculture and Economic Development Analysis Division in Rome, 26–28 June 2002.* FAO. [https://www.fao.org/4/y4249e/y4249e06.htm](https://www.fao.org/4/y4249e/y4249e06.htm)  
- World Health Organization, 2025. Length/height-for-age — WHO Child Growth Standards. [https://www.who.int/tools/child-growth-standards/standards/length-height-for-age](https://www.who.int/tools/child-growth-standards/standards/length-height-for-age)  

