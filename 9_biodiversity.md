---
title: "9. Biodiversity"
layout: default
parent: Model Overview
nav_order: 9
math: katex
description: the biodiversity section of felix
---

# 9. Biodiversity
The biodiversity module is a simple structure representing population carrying capacity. The population is represented by global and encompassing all biomes mean species abundance ($$MSA$$). $$MSA$$ is increased by species regeneration rate ($$Spec\_Regen$$) and decreased by species extinction rate ($$Spec\_Extn$$). In addition, $$MSA$$ approaching species carrying capacity ($$Spec\_Capa$$) limits $$Spec\_Regen$$ and intensifies $$Spec\_Extn$$. This process is quantified as logistic functions and based on the ratio between $$MSA$$ and $$Spec\_Capa$$, and the regeneration factor and the extinction factor, respectively.

## 9.1 Species carrying capacity
$$Spec\_Capa$$ is calculated based on reference species carrying capacity ($$Spec\_Capa\_Max$$), representing maximum sustained population size, and influencing factors related to fertilizers consumption ($$Imp\_Fertz\_on\_Biodiv$$), biomass production for energy purposes ($$Imp\_Biom\_on\_Biodiv$$), climate damage ($$Imp\_CC\_on\_Biodiv$$) and land use change ($$Imp\_Land\_on\_Biodiv$$).

$$
Spec\_Capa(t) = 
    Spec\_Capa\_Max \times 
    Imp\_Fertz\_on\_Biodiv(t) \times 
    Imp\_Biom\_on\_Biodiv(t) \times
    Imp\_CC\_on\_Biodiv(t) \times
    Imp\_Land\_on\_Biodiv(t)
$$

(Eq. 9.1)

The four influencing factors are estimated by logistic functions. In detail, $$Imp\_Fertz\_on\_Biodiv$$ is a logistic function of fertilizer consumption (including nitrogen, phosphate, and potash fertilizers). $$Imp\_Biom\_on\_Biodiv$$ consists of impacts from forest agriculture biomass production, which are logistic functions of related land areas. $$Imp\_CC\_on\_Biodiv$$ is adopted from climate impact on economy, as a logistic function of temperature change from preindustrial. $$Imp\_Land\_on\_Biodiv$$ takes into consideration changes of agricultural land, forest land, and other land compared to their initial areas.

