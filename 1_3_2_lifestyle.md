---
title: "2. Lifestyle"
layout: default
parent: FeliX-Lifestyle
nav_order: 2
math: katex
description: the lifestyle section of FeliX-Lifestyle
---

# 2. Lifestyle

The lifestyle module adapts the LIFE framework developed by Pettifor et al. (2023), which represents lifestyles through interactions between cognition, behaviour, and the social and material contexts that enable or constrain low-carbon behavior. Four lifestyle types - *Resourceful*, *Active*, *Cautious*, and *Constrained* - are represented, with low-carbon behaviours classified using the Avoid-Shift-Improve (ASI) typology across mobility, food, and homes. In FeliX, socioeconomic context determines the population distribution across lifestyle types, feedbacks between cognition and behaviour shape lifestyle-specific behavioural propensities, and these dynamics together are linked to residential energy, passenger transport, and food demand.

## 2.1. Estimating the distribution of lifestyles in the population

The lifestyle module uses outputs from the FeliX economy, education, and population modules to represent changes in the population distribution across the four lifestyle types. This corresponds to the *opportunity effect* in the LIFE framework (Pettifor et al., 2024). Global GDP per capita, population mean age, and the share of the population with at least secondary education represent income, age, and educational attainment, respectively.

These variables are generated endogenously in FeliX. The economy module computes GDP using a Cobb-Douglas production function, the education module tracks the fraction of the population attaining secondary or higher education, and the population module represents ageing through a cohort-based ageing chain with 5-year age bins (Ye et al., 2024). Mean age is used to estimate the age effect.

Reference values for all three drivers are anchored to 2020 levels in the survey data underlying Pettifor et al. (2024). At each model time step, FeliX-derived values are compared with the reference values to estimate the predictors used in the lifestyle-share regression equations. *Resourceful*, *Cautious*, and *Constrained* shares are estimated directly as:

$$ \mathit{Pr}_{l} = \alpha_{l} + \beta_{a,l}Age(t) \times \beta_{i,l}Income(t) \times \beta_{e,l}Education(t) $$

(Eq. 2.1)

where
$$l \in \{Resourceful,\ Cautious,\ Constrained\}$$;
$$\mathit{Pr}_{l}$$ is the percentage of lifestyle type $$l$$;
$$\alpha_{l}$$ is the intercept term for the opportunity effect for lifestyle type $$l$$; and
$$\beta_{a,l}$$, $$\beta_{i,l}$$, and $$\beta_{e,l}$$ are the lifestyle-specific beta coefficients for the age, income, and educational-attainment predictors, respectively.

The *Active* share is calculated as the residual:

$$ Active(t) = 100 - [Resourceful(t) + Cautious(t) + Constrained(t)] $$

(Eq. 2.2)

This ensures that the four lifestyle shares sum to 100% at each model time step.

### Calibration approach

The regression coefficients for *Resourceful*, *Cautious*, and *Constrained* were relatively scaled to align the predicted shares with the reference outputs while maintaining the qualitative lifestyle narratives under the Base scenario with no climate damage. The income term is strongest for *Resourceful*, while the age sensitivity is stronger for *Cautious* than for *Constrained*. *Active* is implicitly calibrated as the residual of the other three lifestyle shares.

## 2.2. Behaviour-cognition feedback

The bidirectional relationship between behaviour and cognition is based on the empirically determined regression equations in the LIFE framework (Pettifor et al., 2024). In FeliX, two coupled stock variables, *Behavior* and *Cognition*, represent the characteristics of the four lifestyle types.

*Behavior* is a normalized value from 0 to 1 representing the propensity to engage in sustainable demand-side mitigation actions, disaggregated by lifestyle, sector, and ASI action:

$$ B_{l,s,a} $$

where
$$l \in \{Active,\ Resourceful,\ Cautious,\ Constrained\}$$;
$$s \in \{mobility,\ food,\ homes\}$$; and
$$a \in \{avoid,\ shift,\ improve\}$$.

### Identity effect

Behaviour accumulates as a function of the *identity effect*, representing cognitive alignment with low-carbon behaviour:

$$ \frac{dB_{l,s,a}(t)}{dt} = r_{l,s,a}^{id}\left(IE_{l,s,a}(t) - B_{l,s,a}(t)\right) $$

(Eq. 2.3)

$$ B_{l,s,a}(t_{0}) = B_{l,s,a}^{0} $$

(Eq. 2.4)

where
$$B_{l,s,a}(t)$$ is the behaviour stock, representing the normalized propensity of lifestyle $$l$$ to undertake ASI action $$a$$ in sector $$s$$;
$$IE_{l,s,a}(t)$$ is the identity effect on behaviour;
$$r_{l,s,a}^{id}$$ is the slope variation parameter;[^1]
$$B_{l,s,a}^{0}$$ is the initial behaviour stock;
$$l \in \{Active,\ Resourceful,\ Cautious,\ Constrained\}$$;
$$s \in \{mobility,\ food,\ homes\}$$; and
$$a \in \{avoid,\ shift,\ improve\}$$.

For each lifestyle, sector, and ASI action, the identity effect is calculated as a linear function of the cognition dimensions:

$$ IE_{l,s,a}(t) = \alpha_{l,s,a} + \sum_{d}\beta_{l,s,a,d}\,C_{d,l}(t) $$

(Eq. 2.5)

where
$$IE_{l,s,a}(t)$$ is the identity effect on behaviour;
$$\alpha_{l,s,a}$$ is the identity-effect intercept;
$$\beta_{l,s,a,d}$$ is the regression coefficient linking cognition dimension $$d$$ to behaviour;
$$C_{d,l}(t)$$ is the cognition value for dimension $$d$$ and lifestyle $$l$$; and
$$d \in \{PBC,\ Values,\ Health,\ EnvBeliefs\}$$.


For calibration to the reference outputs between 2020 and 2050, sector-specific behaviour propensities are aggregated to lifestyle-specific ASI propensities using sector weights $$w_s$$:

$$ ASIPropensity_{l,a} = \frac{\sum_{s}w_{s}\,B_{l,s,a}}{\sum_{s}w_{s}} $$

(Eq. 2.6)

where
$$ASIPropensity_{l,a}$$ is the aggregate behaviour propensity for lifestyle $$l$$ and ASI action $$a$$;
$$w_s$$ is the weight assigned to sector $$s$$; and
$$B_{l,s,a}$$ is the sector-specific behaviour propensity.

The sector weights allow future scenario narratives to vary the relative importance of sectors across ASI actions. They are assumed to be equal in the current analysis.

The initial behaviour stock is constructed by distributing the 2020 reference aggregate lifestyle-ASI propensity across sectors using sectoral shares and normalizing by the sector weights:

$$ B_{l,s,a}^{0} = refB0_{l,a}\,shareB0_{l,s,a}\, \frac{\sum_{s}w_{s}}{\sum_{s}w_{s}\,shareB0_{l,s,a}} $$

(Eq. 2.7)

where
$$B_{l,s,a}^{0}$$ is the initial sector-specific behaviour stock;
$$refB0_{l,a}$$ is the 2020 reference aggregate behaviour propensity for lifestyle $$l$$ and ASI action $$a$$;
$$shareB0_{l,s,a}$$ is the sectoral share used to distribute the aggregate reference propensity across sectors; and
$$w_s$$ is the sector weight.

### Experience effect

*Cognition* is represented as a set of normalized values from 0 to 1 for each lifestyle:

$$ C_{d,l} $$

where
$$C_{d,l}$$ is the cognition value for dimension $$d$$ and lifestyle $$l$$;
$$d \in \{PBC,\ Values,\ Health,\ EnvBeliefs\}$$; and
$$l \in \{Active,\ Resourceful,\ Cautious,\ Constrained\}$$.

Cognition accumulates analogously to behaviour and is driven by the *experience effect*:

$$ \frac{dC_{d,l}(t)}{dt} = r_{d,l}^{\exp}\left(EE_{d,l}(t) - C_{d,l}(t)\right) $$

(Eq. 2.8)

$$ C_{d,l}(t_{0}) = C_{d,l}^{0} $$

(Eq. 2.9)

where
$$C_{d,l}(t)$$ is the cognition stock for dimension $$d$$ and lifestyle $$l$$;
$$EE_{d,l}(t)$$ is the experience effect on cognition;
$$r_{d,l}^{\exp}$$ is the experience adjustment rate;
$$C_{d,l}^{0}$$ is the initial cognition stock;
$$d \in \{PBC,\ Values,\ Health,\ EnvBeliefs\}$$; and
$$l \in \{Active,\ Resourceful,\ Cautious,\ Constrained\}$$.

The cognition stock is initialized from the LIFE dataset as the unweighted mean of each cognition dimension $$d$$ within each lifestyle cluster $$l$$.

The experience effect is calculated as a linear function of behaviour propensities across sectors and ASI actions:

$$ EE_{d,l}(t) = \gamma_{d,l} + \sum_{a}\delta_{d,l,a}\left(\sum_{s}B_{l,s,a}(t)\right) $$

(Eq. 2.10)

where
$$EE_{d,l}(t)$$ is the experience effect on cognition dimension $$d$$ for lifestyle $$l$$;
$$\gamma_{d,l}$$ is the experience-effect intercept;
$$\delta_{d,l,a}$$ is the regression coefficient linking behaviour for ASI action $$a$$ to cognition;
$$B_{l,s,a}(t)$$ is the behaviour propensity for lifestyle $$l$$, sector $$s$$, and ASI action $$a$$;
$$s \in \{mobility,\ food,\ homes\}$$; and
$$a \in \{avoid,\ shift,\ improve\}$$.


### Calibration approach

Selected regression parameters were calibrated to maintain consistency with the LIFE lifestyle typology and the empirical reference trajectories. Aggregate Avoid and Improve behaviour propensities were aligned with their reported reference values for 2020-2050 in Pettifor et al. (2024). For Shift and Cognition, where quantitative reference outputs were not available, calibration preserved the qualitative ordering across lifestyle types. The resulting ordering is *Resourceful* > *Active* > *Cautious* > *Constrained* for cognition and Improve, and *Resourceful* > *Active* > *Constrained* > *Cautious* for aggregate Avoid and Shift, with sectoral differences retained.

## 2.3. Estimation of impacts on residential and passenger transport energy and food consumption

The demand impacts are estimated by combining sectoral ASI behaviour propensities with the population distribution across lifestyle types. The number of adopters for each lifestyle-sector-ASI combination is:

$$ N_{l,s,a}(t) = P(t)\,\mathit{Pr}_{l}(t)\,B_{l,s,a}(t) $$

(Eq. 2.11)

where
$$N_{l,s,a}(t)$$ is the number of adopters in lifestyle $$l$$, sector $$s$$, and ASI action $$a$$;
$$P(t)$$ is total population;
$$\mathit{Pr}_{l}(t)$$ is the population share of lifestyle $$l$$;
$$B_{l,s,a}(t)$$ is the behaviour propensity for lifestyle $$l$$, sector $$s$$, and ASI action $$a$$;
$$l \in \{Active,\ Resourceful,\ Cautious,\ Constrained\}$$;
$$s \in \{mobility,\ food,\ homes\}$$; and
$$a \in \{avoid,\ shift,\ improve\}$$.


Total population-wide adopters for a sector-action are:

$$ N_{s,a}(t) = \sum_{l}N_{l,s,a}(t) $$

(Eq. 2.12)

where $$N_{s,a}(t)$$ is the total number of adopters of ASI action $$a$$ in sector $$s$$, aggregated across all lifestyle types.

### 2.3.1. Common ASI implementation structure in energy sectors

Reductions in mobility (passenger transport) and homes (residential energy) are calculated using exogenous estimates of reductions in per-capita energy consumption or energy-use intensity for specific ASI measures. The two sectors use the same accounting structure: baseline sectoral energy consumption from the FeliX energy module, per-adopter savings for each ASI action, aggregate savings across lifestyles, and sequential estimation of post-ASI energy consumption.

For baseline sectoral energy consumption $$E_s(t)$$ and each ASI action $$a \in \{avoid,\ shift,\ improve\}$$, total savings are:

$$ S_{a}(t) = \sum_{l}N_{l,s,a}(t)\,s_{a}(t) $$

(Eq. 2.13)

where
$$S_a(t)$$ is the total saving associated with ASI action $$a$$;
$$N_{l,s,a}(t)$$ is the number of adopters from lifestyle $$l$$ in sector $$s$$ and ASI action $$a$$;
$$s_a(t)$$ is the per-adopter saving associated with ASI action $$a$$;
$$l$$ denotes lifestyle type; and
$$a \in \{avoid,\ shift,\ improve\}$$.


Post-ASI sectoral energy consumption is calculated sequentially:

$$ E_{s}^{(A)}(t) = E_{s}(t) - S_{A}(t) $$

(Eq. 2.14)

$$ E_{s}^{(AS)}(t) = E_{s}^{(A)}(t) - S_{S}(t) $$

(Eq. 2.15)

$$ E_{s}^{(ASI)}(t) = E_{s}^{(AS)}(t) - S_{I}(t) $$

(Eq. 2.16)

where
$$E_s(t)$$ is baseline energy consumption in sector $$s$$;
$$E_s^{(A)}(t)$$ is sectoral energy consumption after Avoid;
$$E_s^{(AS)}(t)$$ is sectoral energy consumption after Avoid and Shift;
$$E_s^{(ASI)}(t)$$ is sectoral energy consumption after Avoid, Shift, and Improve; and
$$S_A(t)$$, $$S_S(t)$$, and $$S_I(t)$$ are the aggregate savings from Avoid, Shift, and Improve, respectively.

Table 1 summarizes the ranges used to parameterize the residential and passenger-transport ASI savings.

**Table 1. Assumed reduction potentials for ASI measures in energy demand sectors**

| Sector | ASI action | Specific measure considered | Savings metric | Range of reduction potentials | Sources |
|---|---|---|---|---|---|
| Homes | Avoid | Floor-space sufficiency | Reduction in per-capita floor space (m²/person-yr) | 0-6 m²/person (central: 3 m²/person)[^2] | Rao & Min (2017); Rao et al. (2019); Millward-Hopkins et al. (2020); Kikstra et al. (2021) |
| Homes | Shift | Heat-pump adoption | Percentage reduction in per-capita energy consumption | 31-47% (central: 38%) | Wilson et al. (2024); Bernard et al. (2024) |
| Homes | Improve | Light to moderate envelope retrofits affecting the thermal energy share of end use (space and water heating/cooling) | Percentage reduction in per-capita energy consumption | 18-45% (conservative: 20%)[^3] | Ali et al. (2020); Nägeli et al. (2018); Nematchoua et al. (2021) |
| Mobility | Avoid | Compact city design and transit-oriented development; teleworking measures | Percentage reduction in per-capita kilometres travelled | 2-24% (central: 11%) | Fulton et al. (2021); Zhang & Zhang (2021); Keall et al. (2018) |
| Mobility | Shift | Public-transit adoption | Percentage reduction in per-capita energy consumption | 8-25% (conservative: 10%)[^3] | Aggarwal & Jain (2016); Allena-Ozolina et al. (2022); Kenworthy & Svensson (2022) |
| Mobility | Improve | Improvement in fuel economy due to adoption of hybrid electric vehicles | Percentage reduction in per-capita energy consumption | 23-43% (central: 33%) | Huang et al. (2019) |

Central or conservative values from these ranges are used for the baseline ASI reductions, while the full ranges inform the sensitivity analysis.

### 2.3.2. Food sector outcomes under dietary Shift and Avoid

The food sector represents two behavioural levers: *Shift* and *Avoid*.[^4] Shift replaces the reference diet composition of adopters with a less resource-intensive flexitarian diet. Avoid reduces food demand by eliminating food waste attributable to consumers. In both cases, adoption depends on the population distribution across lifestyles and the lifestyle-specific behaviour propensities.

Let $$l$$ denote lifestyle group and $$f$$ denote food category. The number of adopters of each food behaviour is:

$$ A_{l}^{shift} = P \cdot s_{l} \cdot b_{l,food,shift} $$

(Eq. 2.17)

$$ A_{l}^{avoid} = P \cdot s_{l} \cdot b_{l,food,avoid} $$

(Eq. 2.18)

where
$$A_l^{shift}$$ and $$A_l^{avoid}$$ are the numbers of Shift and Avoid adopters in lifestyle $$l$$;
$$P$$ is total population;
$$s_l$$ is the population share of lifestyle $$l$$;
$$b_{l,food,a}$$ is the propensity of lifestyle $$l$$ to adopt food behaviour $$a$$;
$$l \in \{Active,\ Resourceful,\ Cautious,\ Constrained\}$$; and
$$a \in \{shift,\ avoid\}$$.


Aggregating across lifestyles gives:

$$ A^{shift} = \sum_{l}A_{l}^{shift} $$

(Eq. 2.19)

$$ A^{avoid} = \sum_{l}A_{l}^{avoid} $$

(Eq. 2.20)

where
$$A^{shift}$$ is the total number of dietary Shift adopters across all lifestyles; and
$$A^{avoid}$$ is the total number of food Avoid adopters across all lifestyles.

Dietary Shift is first represented in caloric terms by food category and is then translated into physical food demand in tonnes. Average daily caloric intake per capita is determined endogenously in the broader Diet Change module of FeliX. The reference diet is based on FAO-derived global average dietary composition (FAOSTAT, 2016), while the flexitarian diet corresponds to the EAT-Lancet diet composition (Springmann et al., 2018).

**Table 2. Diet composition parameters for modelling food-sector Shift impacts**

| Food category | Reference diet (% of daily calories) | Flexitarian diet (% of daily calories) |
|---|---:|---:|
| Pasture meat | 1.86 | 0.45 |
| Crop meat | 5.82 | 2.52 |
| Dairy | 6.76 | 7.98 |
| Eggs | 1.19 | 0.76 |
| Pulses | 2.35 | 7.06 |
| Grains | 47.80 | 27 |
| Vegetables & fruits | 8.23 | 12.06 |
| Other crops | 26 | 38.43 |

Let $$C$$ denote average daily caloric intake per capita, $$ref_f$$ the reference diet share of food category $$f$$, and $$flex_f$$ the flexitarian diet share. Per-capita daily caloric demand by food category is:

$$ c_{f}^{ref} = C \cdot ref_{f} $$

(Eq. 2.21)

$$ c_{f}^{flex} = C \cdot flex_{f} $$

(Eq. 2.22)

where
$$c_f^{ref}$$ is the reference per-capita daily caloric demand for food category $$f$$;
$$c_f^{flex}$$ is the flexitarian per-capita daily caloric demand for food category $$f$$;
$$C$$ is average daily caloric intake per capita;
$$ref_f$$ is the reference diet share of food category $$f$$;
$$flex_f$$ is the flexitarian diet share of food category $$f$$; and
$$f$$ denotes food category.

Non-adopters of dietary Shift are:

$$ A^{non} = P - A^{shift} $$

(Eq. 2.23)

where $$A^{non}$$ is the number of non-adopters of dietary Shift.

Annual baseline caloric demand by category, before dietary Shift, is:

$$ Q_{f}^{bef\_shift} = c_{f}^{ref} \cdot P \cdot 365 $$

(Eq. 2.24)

Annual caloric demand after Shift is:

$$ Q_{f}^{aft\_shift} = c_{f}^{flex} \cdot A^{shift} \cdot 365 + c_{f}^{ref} \cdot A^{non} \cdot 365 $$

(Eq. 2.25)

The resulting change in caloric demand by food category is:

$$ \Delta Q_{f}^{shift} = Q_{f}^{bef\_shift} - Q_{f}^{aft\_shift} $$

(Eq. 2.26)

where
$$Q_f^{bef\_shift}$$ is annual baseline caloric demand for food category $$f$$ before dietary Shift;
$$Q_f^{aft\_shift}$$ is annual caloric demand for food category $$f$$ after dietary Shift;
$$\Delta Q_f^{shift}$$ is the change in caloric demand attributable to dietary Shift;
$$A^{shift}$$ and $$A^{non}$$ are the numbers of Shift adopters and non-adopters, respectively; and
$$365$$ converts daily caloric demand to annual caloric demand.

Let $$k_f$$ denote caloric value per tonne of food category $$f$$, $$w_f$$ the waste fraction attributed to food production, and $$\lambda_f$$ the loss fraction of effective demand. The reduction in food demand attributable to Shift is:

$$ \Delta D_{f}^{shift} = \frac{\Delta Q_{f}^{shift}}{(1-w_{f})\,k_{f}\,(1-\lambda_{f})} $$

(Eq. 2.27)

where
$$\Delta D_f^{shift}$$ is the reduction in physical food demand attributable to dietary Shift;
$$\Delta Q_f^{shift}$$ is the corresponding change in caloric demand;
$$w_f$$ is the food-waste fraction attributed to production;
$$k_f$$ is the caloric value per tonne of food category $$f$$; and
$$\lambda_f$$ is the food-loss fraction of effective demand.

Avoid behaviour represents a reduction in food demand from eliminating food waste attributable to consumers. Let $$\omega_f$$ denote the reference consumer-attributed waste fraction for food category $$f$$. The avoidable daily caloric demand per capita is:

$$ c_{f}^{avoid} = c_{f}^{ref} \cdot \omega_{f} $$

(Eq. 2.28)

where
$$c_f^{avoid}$$ is the avoidable daily caloric demand per capita for food category $$f$$;
$$c_f^{ref}$$ is the reference daily caloric demand per capita for food category $$f$$; and
$$\omega_f$$ is the consumer-attributed waste fraction for food category $$f$$.

The annual caloric demand avoided by adopters is:

$$ Q_{f}^{avoid} = c_{f}^{avoid} \cdot A^{avoid} \cdot 365 $$

(Eq. 2.29)

where
$$Q_f^{avoid}$$ is the annual caloric demand avoided for food category $$f$$;
$$c_f^{avoid}$$ is avoidable daily caloric demand per capita;
$$A^{avoid}$$ is the total number of Avoid adopters; and
$$365$$ converts daily caloric demand to annual caloric demand.

This quantity represents food that would otherwise have been wasted at the consumer end of the supply chain and is therefore not reduced by the food-waste fraction again. Conversion into production-equivalent physical demand still accounts for upstream food losses:

$$ \Delta D_{f}^{avoid} = \frac{Q_{f}^{avoid}}{k_{f}\,(1-\lambda_{f})} $$

(Eq. 2.30)

where
$$\Delta D_f^{avoid}$$ is the reduction in physical food demand attributable to Avoid;
$$Q_f^{avoid}$$ is the annual avoided caloric demand;
$$k_f$$ is the caloric value per tonne of food category $$f$$; and
$$\lambda_f$$ is the food-loss fraction of effective demand.

For downstream land-use calculations, Shift and Avoid are combined sequentially in a single final food-demand expression:

$$ F_{f}^{final} = \frac{\frac{Q_{f}^{shift}}{1-w_{f}} - Q_{f}^{avoid}}{k_{f}(1-\lambda_{f})} $$

(Eq. 2.31)

where
$$F_f^{final}$$ is final food demand for food category $$f$$ in tonnes;
$$Q_f^{shift}$$ is caloric demand after dietary Shift;
$$w_f$$ is the food-waste fraction attributed to production;
$$Q_f^{avoid}$$ is the annual caloric demand avoided through consumer food-waste reduction;
$$k_f$$ is the caloric value per tonne of food category $$f$$; and
$$\lambda_f$$ is the food-loss fraction of effective demand.

Dietary Shift first changes the composition of caloric demand across food categories. The shifted demand is then adjusted for the food-waste fraction attributed to production. Avoid is subsequently subtracted directly because it represents recovery of consumer-attributed food waste. The resulting net caloric demand is converted into physical food demand in tonnes by accounting for caloric density and upstream food losses.

[^1]: The slope variation parameter is introduced as a multiplicative lever to enable future scenario narratives that vary the rate of growth of behaviour propensities for specific lifestyle-sector-ASI combinations.

[^2]: The floor-space range is estimated as the difference between FeliX reference-scenario per-capita floor space and target or minimum per-capita floor space from the sufficiency literature. Because the FeliX reference scenario accounts for climate damages and has lower per-capita floor-space growth than the cited studies, a conservative range is used.

[^3]: A conservative end of the range is used because estimates vary substantially with baseline activity assumptions.

[^4]: Improve measures are primarily represented in upstream food-sector processes, including resource efficiency, sustainable farming practices, processing technology, and supply-chain logistics. The lifestyle module therefore focuses on individually driven consumer change.

## References

- Aggarwal, P., & Jain, S. (2016). Energy demand and CO2 emissions from urban on-road transport in Delhi: Current and future projections under various policy measures. Journal of Cleaner Production, 128, 48-61.
- Ali, U., Shamsi, M. H., Bohacek, M., Hoare, C., Purcell, K., Mangina, E., & O’Donnell, J. (2020). A data-driven approach to optimize urban scale energy retrofit decisions for residential buildings. Applied Energy, 267, 114861.
- Allena-Ozolina, S., Pakere, I., Jaunzems, D., Freimanis, R., Blumberga, A., & Bazbauers, G. (2022). Passenger transport shift to green mobility assessment using TIMES model. Rīgas Tehniskās Universitātes Zinātniskie Raksti, 26(1), 341-356.
- Bernard, L., Hackett, A., Metcalfe, R. D., & Schein, A. (2024). Decarbonizing heat: The impact of heat pumps and a time-of-use heat pump tariff on energy demand (Working Paper No. 33036). National Bureau of Economic Research.
- FAOSTAT. (2016). Food balance sheets [Data set]. Food and Agriculture Organization of the United Nations.
- Fulton, L., Reich, D. T., Ahmad, M., Circella, G., & Mason, J. (2021). The compact city scenario-electrified: The only way to 1.5°C [Report]. Institute for Transportation and Development Policy; University of California, Davis, Institute of Transportation Studies.
- Huang, Y., Surawski, N. C., Organ, B., Zhou, J. L., Tang, O. H., & Chan, E. F. (2019). Fuel consumption and emissions performance under real driving: Comparison between hybrid and conventional vehicles. Science of the Total Environment, 659, 275-282.
- Keall, M. D., Shaw, C., Chapman, R., & Howden-Chapman, P. (2018). Reductions in carbon dioxide emissions from an intervention to promote cycling and walking: A case study from New Zealand. Transportation Research Part D: Transport and Environment, 65, 687-696.
- Kenworthy, J. R., & Svensson, H. (2022). Exploring the energy saving potential in private, public and non-motorized transport for ten Swedish cities. Sustainability, 14(2), 954.
- Kikstra, J. S., Mastrucci, A., Min, J., Riahi, K., & Rao, N. D. (2021). Decent living gaps and energy needs around the world. Environmental Research Letters, 16(9), 095006.
- Millward-Hopkins, J., Steinberger, J. K., Rao, N. D., & Oswald, Y. (2020). Providing decent living with minimum energy: A global scenario. Global Environmental Change, 65, 102168.
- Nägeli, C., Camarasa, C., Jakob, M., Catenazzi, G., & Ostermeyer, Y. (2018). Synthetic building stocks as a way to assess the energy demand and greenhouse gas emissions of national building stocks. Energy and Buildings, 173, 443-460.
- Nematchoua, M. K., Nishimwe, A. M. R., & Reiter, S. (2021). Towards nearly zero-energy residential neighbourhoods in the European Union: A case study. Renewable and Sustainable Energy Reviews, 135, 110198.
- Pettifor, H., Agnew, M., & Wilson, C. (2023). A framework for measuring and modelling low-carbon lifestyles. Global Environmental Change, 82, 102739.
- Pettifor, H., Mastrucci, A., Wilson, C., van Ruijven, B., Agnew, M., & Le Gallic, T. (2024). Endogenous simulation of low-carbon lifestyle change in global climate mitigation pathways. Environmental Research Letters, 19(1), 014016. https://doi.org/10.1088/1748-9326/acf6d6
- Rao, N. D., & Min, J. (2017). Decent living standards: Material prerequisites for human wellbeing. Social Indicators Research. https://doi.org/10.1007/s11205-017-1650-0
- Rao, N. D., Min, J., & Mastrucci, A. (2019). Energy requirements for decent living in India, Brazil and South Africa. Nature Energy, 4(12), 1025-1032.
- Springmann, M., Clark, M., Mason-D’Croz, D., Wiebe, K., Bodirsky, B. L., Lassaletta, L., … Willett, W. (2018). Options for keeping the food system within environmental limits. Nature, 562(7728), 519-525. https://doi.org/10.1038/s41586-018-0594-0
- Wilson, E. J., Munankarmi, P., Less, B. D., Reyna, J. L., & Rothgeb, S. (2024). Heat pumps for all? Distributions of the costs and benefits of residential air-source heat pumps in the United States. Joule, 8(4), 1000-1035.
- Ye, Q., Liu, Q., Swamy, D., Gao, L., Moallemi, E. A., Rydzak, F., & Eker, S. (2024). FeliX 2.0: An integrated model of climate, economy, environment, and society interactions. Environmental Modelling & Software, 179, 106121.
- Zhang, R., & Zhang, J. (2021). Long-term pathways to deep decarbonization of the transport sector in the post-COVID world. Transport Policy, 110, 28-36.