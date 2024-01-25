---
title: "3. Energy"
layout: default
parent: Model Overview
nav_order: 3
math: katex
description: the energy section of felix
---

# 3. Energy
The energy module in FeliX includes total energy demand and energy supply from different fossil fuels (oil, gas, coal) and renewable energy (wind, solar, biomass).

## 3.1. Energy demand
Global total energy demand ($$En\_Dem\_Tot$$) is determined by the per-capita energy demand and the global population. The energy demand per capita ($$En\_Dem\_per\_Cap$$) is determined by the wealth of the population.

$$
En\_Dem\_per\_Cap(t) = Imp\_GWP\_on\_En\_Dem(t) \times En\_Dem\_per\_Cap\_Max
$$

(Eq. 3.1)

$$Imp\_GWP\_on\_En\_Dem$$ represents the impact of $$GWP$$ on $$En\_Dem\_per\_Cap$$. It is modeled as a non-linear relationship―initially increasing at a low rate, then at an increased rate and eventually flattens out over the long run. Furthermore, $$Imp\_GWP\_on\_En\_Dem$$ is calibrated according to the historical energy demand pattern obtained from Energy Institute (2023). $$En\_Dem\_per\_Cap\_Max$$ is the maximal reference of energy demand per capita.

## 3.2. Energy production
Energy production comes from three fossil fuels (coal, oil, and gas) and three renewable (solar, wind, and biomass) sources, to meet the total energy demand. The production of any type of energy is determined by its identified resource and production capacity, and its market share.

### Energy production from fossil fuels

The production of fossil fuels is modeled as a supply chain structure, adapted from Sterman and Richardson (1985) and Davidsen et al. (1990). This section uses oil as an example to explain main components of the energy production structure for fossil fuels. In general, oil is produced from identified oil resources, which grows based on oil exploration through existing technologies from undiscovered oil resources.

Oil exploration ($$Expl_{oil}$$) is counted as the lower value of a potential exploration rate of oil ($$Expl\_Pot_{oil}$$) and a desired exploration rate of oil ($$Expl\_Des_{oil}$$).

$$
Expl_{oil}(t) = MIN(Expl\_Pot_{oil},Expl\_Des_{oil})
$$

(Eq. 3.2)

 $$Expl\_Pot_{oil}$$ represents the exploration possible due to effective investments in oil exploration ($$Eff\_Expl\_Inv_{oil}$$) and productivity of available technologies ($$Prodvty\_Expl\_Inv_{oil}$$) which encapsulates the resource depletion effect.

$$
Expl\_Pot_{oil}(t) = Eff\_Expl\_Inv_{oil}(t) \times Prodvty\_Expl\_Inv_{oil}(t)
$$

(Eq. 3.3)

$$Expl\_Des_{oil}$$ represents the amount of oil resources that would ensure continued production at the current rate. Unit cost of oil exploration is then estimated depending on the remaining undiscovered oil resources and advances in exploration technologies. The cost of oil exploration in turn determines the desired investment in oil exploration.

Similarly, the oil production is counted as the lower value of either total oil demand ($$En\_Dem_{oil}$$) or a potential oil production rate ($$Prod\_Pot_{oil}$$).

$$
Prod_{oil}(t) = MIN(En\_Dem_{oil}(t),Prod\_Pot_{oil}(t))
$$

(Eq. 3.4)

$$En\_Dem_{oil}$$ is calculated as the market share of oil ($$MS_{oil}$$) in total energy demand ($$En\_Dem\_Tot$$).

$$
En\_Dem_{oil}(t) = En\_Dem\_Tot(t) \times MS_{oil}(t)
$$

(Eq. 3.5)

The potential oil production rate equals to the production due to effective investments in oil production and available resources. Similar to the costs of exploration, the unit cost of oil production is then dependent on the productivity of investment in oil production which encapsulates the resource availability effect. It is important to note that production costs also include the policy-set carbon price. The cost of both oil exploration and production determines the oil price, which affects the market share of oil demand in total energy demand (see section **3.3 Market shares of energy sources in total energy demand**).


### Energy production from renewable sources

There are several main factors that affect the production of renewable energy from wind, solar, and biomass sources. They are resource characteristics (e.g., average sun radiation for solar energy), efficiency and aging of technology, land availability, installation cost, investment in installation and efficiency, and the impact of technological learning on unit costs of installation. This section uses solar energy as an example to explain important dynamics in the structure underlying renewable energy production.

Firstly, total solar demand equals to the market share of solar energy ($$MS_{solar}$$) multiplied by the total energy demand.

$$
En\_Dem_{solar}(t) = En\_Dem\_Tot(t) \times MS_{solar}(t)
$$

(Eq. 3.6)

Secondly, the solar production capacity is calculated to meet total solar demand but constrained by the potential solar energy production.

$$
Prod_{solar}(t) = MIN(En\_Dem_{solar}(t),Prod\_Pot_{solar}(t))
$$

(Eq. 3.7)

The potential solar energy production depends on the available solar resource and technological constraints of average intensity of the resource, annual availability of the resource considering weather impacts, changing efficiency of solar radiation conversion at the current state of technical developments, and the installed capacity to convert solar radiation into energy. The installed solar capacity changes according to the new installation of solar capacity, which is influenced by the productivity of solar investments and the adjustment of existing solar infrastructure. Lastly, the unit cost of solar energy is estimated as a sum of the unit costs of installation and production.

## 3.3 Market shares of energy sources in total energy demand
The total energy demand is allocated to different energy sources based on their respective market shares ($$MS$$). $$MS$$  is calculated based on indicative market shares ($$MS_Ind$$) of energy sources which are defined to represent accumulated market shares of different energy sources over time.

$$
MS_{energy}(t) = 
\frac
    {MS\_Ind_{energy}(t)}
    {\sum_{energy}{MS\_Ind_{energy}(t)}}
$$

(Eq. 3.8)

$$MS\_Ind$$ of a specific energy is determined by effects of price on the market share ($$Eff\_MS\_on\_Price$$) and time to adjust the market share ($$T\_Adj$$).

$$
\frac
    {\,dMS\_Ind_{energy}(t)}
    {\,dt}
= 
\frac
    {MS\_Ref_{energy} \times Eff\_MS\_on\_Price(t) - MS\_Ind_{energy}(t)}
    {T\_Adj}
$$

(Eq. 3.9)

where $$MS\_Ref_{energy}$$ is the reference market share of a specific energy source. $$T\_Adj$$ is set as 10 years for all energy sources. $$Eff\_MS\_on\_Price$$ depends on the competitive price factors and prices of energy sources. The price of each energy source is averaged over a period, and all the prices result in the average energy price. The price competitive factor is calculated for all energy sources as a ratio of the averaged price of each energy source and the average energy price. The price competitive factor is further adjusted by the elasticity of that energy source price to demand.

## References
- Davidsen, P. I., Sterman, J. D., & Richardson, G. P. (1990). A petroleum life cycle model for the United States with endogenous technology, exploration, recovery, and demand. System Dynamics Review, 6(1), 66–93. https://doi.org/10.1002/sdr.4260060105
- Energy Institute, 2023. BP Statistical Review of World Energy (2023).
- Sterman, J. D., & Richardson, G. P. (1985). An experiment to evaluate methods for estimating fossil fuel resources. Journal of Forecasting, 4(2), 197–226. https://doi.org/10.1002/for.3980040208

