---
title: "1. Sectorial Energy Demand"
layout: default
parent: FeliX-Lifestyle
nav_order: 1
math: katex
description: the sectorial energy demand section of FeliX-Lifestyle
---

# 1. Sectorial Energy Demand

FeliX represents global final energy demand from major end-use sectors over 1900-2100 using a hybrid empirical-structural approach. Sectorial formulations differ according to the availability of activity indicators, energy-intensity data, and empirical relationships with economic development. Residential buildings and passenger transport are represented explicitly through activity and energy intensity, while industry, commercial/services, and freight transport are modelled from fitted per-capita energy-consumption trajectories. Sectorial final energy demand is aggregated and converted to primary energy demand using a global average fuel-efficiency factor.

## 1.1. Residential buildings and passenger transport

For residential buildings and passenger transport, final energy consumption is calculated as the product of per-capita activity and energy intensity per unit activity. Activity is modelled as a function of endogenous global GDP per capita using bounded saturation relationships that capture the S-shaped response of activity to rising income and saturation at high income levels.

Per-capita activity in sector $$s$$ is represented as:

$$ A_{s}^{pc}(t) = A_{s,max}(t)\,\frac{x_{s}(t)^{\alpha_{s}}}{x_{s}(t)^{\alpha_{s}} + I_{s}^{\alpha_{s}}},\qquad x_{s}(t) = \frac{G(t)}{G_{ref,s}} $$

(Eq. 1.1)

where
$$t$$ is time in years;
$$s \in \{residential,\ passenger\ transport\}$$;
$$A_{s}^{pc}(t)$$ is per-capita activity in sector $$s$$;
$$G(t)$$ is GDP per capita;
$$G_{ref,s}$$ is the sector-specific reference level of GDP per capita used to calculate the normalized income ratio;
$$A_{s,max}(t)$$ is the sector-specific maximum activity per capita;
$$I_s$$ is the dimensionless half-saturation parameter, corresponding to the value of $$x_s$$ at which activity reaches half of $$A_{s,max}$$; and
$$\alpha_s$$ is the dimensionless steepness parameter governing how rapidly activity approaches the ceiling as income rises.

For residential buildings, activity is represented by floor area per capita. For passenger transport, activity is represented by passenger-kilometres per capita.

Sectorial energy intensity per unit activity, $$e_s(t)$$, is represented by a logistic time trend fitted to historical data:

$$ e_{s}(t) = L_{s} + \frac{U_{s} - L_{s}}{1 + \exp\left(k_{s}\,(t - t_{mid,s})\right)} $$

(Eq. 1.2)

where
$$e_s(t)$$ is energy intensity per unit activity in sector $$s$$;
$$U_s$$ and $$L_s$$ are the upper and lower asymptotes of energy intensity;
$$k_s$$ is the rate parameter governing the speed of change; and
$$t_{mid,s}$$ is the midpoint year at which intensity is halfway between $$U_s$$ and $$L_s$$.

Per-capita final energy consumption is then calculated as:

$$ E_{s}^{pc}(t) = A_{s}^{pc}(t)\,e_{s}(t) $$

(Eq. 1.3)

where
$$E_s^{pc}(t)$$ is per-capita final energy consumption in sector $$s$$;
$$A_s^{pc}(t)$$ is per-capita activity; and
$$e_s(t)$$ is energy intensity per unit activity.

Total sectorial final energy consumption is obtained by scaling per-capita energy use by the endogenous FeliX population:

$$ E_{s}(t) = P(t)\,E_{s}^{pc}(t) $$

(Eq. 1.4)

where
$$E_s(t)$$ is total final energy consumption in sector $$s$$;
$$P(t)$$ is total population; and
$$E_s^{pc}(t)$$ is per-capita final energy consumption.

This activity-intensity structure allows changes in activity and energy intensity to be represented separately. Sectorial parameters are calibrated using IEA Energy End-uses and Efficiency Indicators (EEI), IEA World Energy Balances (WEB), and World Bank GDP and population data (International Energy Agency, 2025a, 2025b; World Bank, 2024a, 2024b).

## 1.2. Industry, commercial services, and freight transport

For industry, commercial/services, and freight transport, final energy consumption is modelled directly as per-capita energy use. Historical global per-capita final energy use is constructed from IEA WEB sectorial energy totals and World Bank population data.

For each sector $$s \in \{industry,\ commercial/services,\ freight\}$$, per-capita energy consumption is calculated from a reference trajectory and a scenario demand multiplier, which is set to 1 for the reference trajectory:

$$ E_{s}^{pc}(t) = E_{s,ref}^{pc}(t)\,M_{s}(t) $$

(Eq. 1.5)

where
$$E_s^{pc}(t)$$ is per-capita final energy consumption in sector $$s$$;
$$E_{s,ref}^{pc}(t)$$ is the sector-specific reference per-capita energy trajectory; and
$$M_s(t)$$ is the sector-specific demand multiplier.

Total final energy consumption is then calculated as:

$$ E_{s}(t) = P(t)\,E_{s}^{pc}(t) $$

(Eq. 1.6)

where
$$E_s(t)$$ is total final energy consumption in sector $$s$$;
$$P(t)$$ is total population; and
$$E_s^{pc}(t)$$ is per-capita final energy consumption.

For commercial/services and freight transport, the reference per-capita trajectory is represented by a logistic function in time:

$$ E_{s,ref}^{pc}(t) = L_{s} + \frac{K_{s} - L_{s}}{1 + \exp\left[-k_{s}\,(t - I_{s})\right]} $$

(Eq. 1.7)

where
$$s \in \{commercial/services,\ freight\}$$;
$$L_s$$ is the lower asymptote of per-capita energy consumption;
$$K_s$$ is the upper asymptote;
$$k_s$$ is the rate parameter governing the speed of change; and
$$I_s$$ is the midpoint year.

For industry, the reference trajectory follows the historical per-capita energy series through 2022 and then approaches a specified long-run target using an exponential adjustment:

$$
E_{industry,ref}^{pc}(t) =
\begin{cases}
E_{industry,hist}^{pc}(t), & t \leq 2022 \\
E_{industry,2022}^{pc} + \left(E_{industry,target}^{pc} - E_{industry,2022}^{pc}\right)
\left[1 - \exp\left(-\frac{t-2022}{90}\right)\right], & t > 2022
\end{cases}
$$

(Eq. 1.8)

where
$$E_{industry,hist}^{pc}(t)$$ is the historical industrial per-capita energy series;
$$E_{industry,2022}^{pc}$$ is the historical 2022 value;
$$E_{industry,target}^{pc}$$ is the specified long-run target level; and
$$90$$ years is the adjustment time scale used in the post-2022 projection.

The logistic and exponential formulations provide bounded long-run trajectories and avoid indefinite extrapolation of short-term trends. The scenario demand multipliers allow the reference trajectories to vary across future scenarios.

## 1.3. Calibration approach

Sectorial trajectories are calibrated to reproduce historical global totals from the IEA WEB over the overlapping historical period, typically 1971-2022, while maintaining empirically defensible long-run behaviour. The formulation therefore combines detailed activity-based representation where data permit, particularly for residential buildings and passenger transport, with empirically constrained aggregate representations for industry, commercial/services, and freight transport.

Country-level IEA EEI data are used as an external reference for long-run constraints. The upper asymptote of each sectorial per-capita energy trajectory is required to remain below the upper tail of observed high-income country values, such as the 95th percentile. Lower asymptotes are similarly constrained by observed minimum global per-capita energy levels. These constraints keep projected trajectories within observed cross-country ranges while preserving calibration to historical global totals.

Passenger transport requires an additional adjustment because the EEI and WEB databases use different transport accounting boundaries. The EEI activity and intensity indicators represent ordinary passenger and freight transport and exclude international aviation and marine bunkers, whereas these fuels are included in the WEB world-total transport series. International bunker energy is therefore added separately to the modelled ordinary transport total. Historical bunker energy is taken from the IEA WEB Extended Database as the sum of world aviation and marine bunkers for 1971-2022, with earlier values back-cast to 1900 (International Energy Agency, 2025c). After the historical period, bunker energy is projected in proportion to modelled ordinary passenger and freight transport energy using the average pre-COVID bunker share over 2015-2019. Total transport energy is then calculated as the sum of ordinary passenger and freight transport energy and international bunker energy, aligning the model with the WEB total-transport accounting boundary.

These sectors are treated as partially exogenous because robust per-capita activity indicators are not available. Future model development may represent income-driven per-capita energy consumption more explicitly.

## References

- International Energy Agency. (2025a). Energy End-uses and Efficiency Indicators [Data set]. Retrieved July 20, 2025, from https://www.iea.org/data-and-statistics/data-product/energy-end-uses-and-efficiency-indicators
- International Energy Agency. (2025b). World Energy Balances [Data set]. Retrieved May 12, 2025, from https://www.iea.org/data-and-statistics/data-product/world-energy-balances
- International Energy Agency. (2025c). World Energy Balances [Extended database]. Retrieved May 12, 2025, from https://www.iea.org/data-and-statistics/data-product/world-energy-balances
- World Bank. (2024a). GDP per capita, PPP (current international $) [Data set]. World Development Indicators. Retrieved June 10, 2025, from https://data.worldbank.org/indicator/NY.GDP.PCAP.PP.CD
- World Bank. (2024b). Population, total [Data set]. World Development Indicators. Retrieved June 10, 2025, from https://data.worldbank.org/indicator/SP.POP.TOTL
