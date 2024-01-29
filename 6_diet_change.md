---
title: "6. Diet change"
layout: default
parent: Model Overview
nav_order: 6
math: katex
description: the diet change section of felix
---

# 6. Diet change
Food demand is quantified based on the total caloric demand for eight main food categories. Total caloric demand is based on dietary choices of different population segments. Population segments of dietary choices are represented by the followers of the meat-based and vegetarian diets for each age cohort and gender (Eker et al., 2019). The shifts between these two dietary choices depend on income (represented by $$GWP\_per\_Cap$$) and social and behavioral factors such as climate and health risk perception, self-efficacy and social norms that underly pro-environmental behavior.

Followers of meat-based and vegetarian diets are assumed to eat a standard mix of eight food categories. We used typical United States’ diets (Pimentel and Pimentel, 2003), a reference world diet and the global average supply statistics, as benchmarks to understand how meat-based and vegetarian diets differ globally. Based on such proportional differences of meat-based and vegetarian diets, we form the reference meat-based and vegetarian diets by decomposing the world’s average diet according to the population fraction of the two groups. Besides reference diets, we also built flexibility in the model to run scenario analyses with flexitarian, healthy-eating, and vegan diets (Springmann et al. 2018).

## 6.1. Caloric demand
Total annual caloric demand for plant-based food ($$Cal\_Dem$$) is the sum of total plant-based caloric intake by the vegetarian population ($$Pop\_Veg$$) and meat-eating population ($$Pop\_Meat$$).

$$
Cal\_Dem_{food}(t) = 
    Intk\_Veg_{food} \times Pop\_Veg(t) + Intk\_Meat_{food} \times Pop\_Meat(t), \text{ where } food \in [\text{pulses, grains, vegetables and fruits, other crops}]   
$$

(Eq. 6.1)

where $$Intk\_Veg$$ and $$Intk\_Meat$$ are the annual per-capita intake of plant-based calories in the vegetarian diet and meat-based diet, respectively. Both are assumed as a constant fraction of the annual total caloric intake per capita ($$Intk\_Tot$$).

$$
Intk\_Veg(t) = \varphi\_Veg \times Intk\_Tot(t)
$$

(Eq. 6.2)

$$
Intk\_Meat(t) = \varphi\_Meat \times Intk\_Tot(t)
$$

(Eq. 6.3)

$$Intk\_Tot$$ is formulated as the multiplication of a reference intake per capita ($$Intk\_Tot\_Ref$$) and the effect of income ($$Imp\_GWP\_on\_Cal$$). 

$$
Intk\_Tot(t) = Intk\_Tot\_Ref \times Imp\_GWP\_on\_Cal(t)
$$

(Eq. 6.4)


$$Imp\_GWP\_on\_Cal$$ is a logistic function based on $$GWP\_per\_Cap$$. 

Total annual caloric demand for animal-based food is simplified as

$$
Cal\_Dem_{food}(t) = 
    Intk\_Meat_{food} \times Pop\_Meat(t), \text{ where } food \in [\text{pasture-based meat, crop-based meat, dairy, eggs}]   
$$

(Eq. 6.5)

where $$Intk\_Meat$$ is the annual per-capita intake of meat-based calories in the meat-based diet. 

It is important to note that Eqs. Eq. 6.1-6.5 are actually defined for each gender and age group, since caloric intake depends on age and gender. $$Intk\_Tot$$ is adjusted for each age cohort and gender based on the estimated calorie needs for moderate activity level. The heterogeneity for physical activity levels, however, is not included because the moderate level represents the average of various activity and consumption levels. 

## 6.2 Food demand and food production
Food demand ($$Food\_Dem_{food}$$) is calculated as $$Cal\_Dem_{food}$$ divided by the caloric value of associated food category. In addition, plant-based food categories can also be used as livestock feed. The amount of plant-based food used for feed depends on crop-based meat demand, feed share of four plant-based food, and unit-feed requirement for livestock. Food production ($$Prod_{food}$$) is eventually steered by waste-adjusted food demand, which is calculated as $$Food\_Dem_{food}$$ divided by a waste fraction ($$\varphi\_Wst$$) of supply.

$$
Prod_{food}(t) = \frac
    {Food\_Dem_{food}(t)}
    {1-\varphi\_Wst}
$$

(Eq. 6.6)

$$\varphi\_Wst$$ is set as 0.30 for grains, 45% for pulses, vegetables and fruits the waste fraction is 45%, and 20% for other food categories.

The production of animal-based food products (pasture-based meat, crop-based meat, dairy, and eggs) follows a similar approach based on grassland availability, food demand and land yield. Dairy production is aligned with meat production, and the production of eggs is formulated with respect to crop-based meat production, which depends on the feed fraction of crop production.

## References
- Eker, S., Reese, G., Obersteiner, M., 2019. Modelling the drivers of a widespread shift to sustainable diets. Nat Sustain 2, 725–735. https://doi.org/10.1038/s41893-019-0331-1
- Pimentel, D., Pimentel, M., 2003. Sustainability of meat-based and plant-based diets and the environment. The American Journal of Clinical Nutrition 78, 660S-663S. https://doi.org/10.1093/ajcn/78.3.660S
- Springmann, M., Clark, M., Mason-D’Croz, D., Wiebe, K., Bodirsky, B.L., Lassaletta, L., De Vries, W., Vermeulen, S.J., Herrero, M., Carlson, K.M., Jonell, M., Troell, M., DeClerck, F., Gordon, L.J., Zurayk, R., Scarborough, P., Rayner, M., Loken, B., Fanzo, J., Godfray, H.C.J., Tilman, D., Rockström, J., Willett, W., 2018. Options for keeping the food system within environmental limits. Nature 562, 519–525. https://doi.org/10.1038/s41586-018-0594-0