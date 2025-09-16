---
title: "4. Water"
layout: default
parent: Global FeliX
nav_order: 4
math: katex
description: the water section of felix
---

# 4. Water
The water module mainly quantifies global average water scarcity, that is, the balance between water availability and use. Water availability is a function of available water resources, water recovery of used water in economic sectors, and a drought rate for the impact of climate change. Total water use considers water withdrawal from economic sectors to meet their water demand.

## 4.1. Water supply and water availability
Available water resources consist of water supply rate of fresh and non-conventional water, water recovery rate of used water resources by the three economic sectors, and drought out rate representing extreme drought events. Water supply is estimated by multiplying desired water supply rate and water supply fulfillment rate (describing water supply fulfillment as a relation of water supply and demand). Desired water supply rate ($$Wat\_Sup\_Des$$) is to cover water consumption ($$Wat\_Cons$$, i.e., water use decreased by recovery of used water resources of three economic sectors) and available water resources adjustment ($$Wat\_Avail\_Adj$$, taking into account dynamics of total water demand and water safety stock coverage).

$$
Wat\_Sup\_Des(t) = MAX(0,Wat\_Cons(t)+Wat\_Avail\_Adj(t))
$$

(Eq. 4.1)

With growing water demand, the supply fulfillment might be impaired which relates to infrastructure design and its operating limits. This relationship is modeled as a logistic function dependent on the amount of water that can be reliably provided ($$Wat\_Sup\_Reli$$) on annual basis for agricultural, industrial, and domestic sectors due to resources and infrastructure availability.

$$
Wat\_Sup\_Fulf(t) = 
\frac
    {2}
    {
        1+
        e^{-Wat\_Sup\_Fulf\_Param \times 
        \frac
            {Wat\_Sup\_Reli(t)}
            {Wat\_Sup\_Des(t)}
        }  
    }
-1
$$

(Eq. 4.2)

where $$Wat\_Sup\_Fulf\_Param$$ determines the strength of infrastructure operating limits on water supply fulfillment. Associated data are obtained from 2030 Water Resources Group (2009).

## 4.2. Water demand, water withdrawal, and water use
Water is demanded for economic production by agriculture, industrial, and domestic sectors. Agricultural water demand ($$Wat\_Dem\_Agri$$) is dependent on two ways of land watering―irrigation and rainfed.

$$
Wat\_Dem\_Agri(t) = Wat\_Int\_Irr(t) \times Area\_Irr(t) + Wat\_Int\_Rfed(t) \times Area\_Rfed(t)
$$

(Eq. 4.3)

where $$Wat\_Int\_Irr$$ and $$Wat\_Int\_Rfed$$ represent average agricultural water demand per square (i.e., water intensity, $$Wat\_Int$$) agricultural land areas of irrigation ($$Area\_Irr$$) or rainfed ($$Area\_Rfed$$), respectively. $$Area\_Irr$$ is calculated by multiplying total agricultural land areas with the percentage of irrigated land areas, which is estimated by considering the impact of wealth (represented by $$GWP\_per\_Cap$$) and their upper and lower limits. This approach is also applied to estimate $$Wat\_Int\_Irr$$, $$Wat\_Int\_Rfed$$, and total water demand for industrial sector based on their own upper and lower limits, respectively. Domestic water demand is quantified based on total population and average domestic water demand per capita. Domestic water demand per capita is estimated by considering the impact of wealth (represented by $$GWP\_per\_Cap$$) and their upper and lower limits.

Agricultural, industrial, and domestic water demand drives water resources withdrawal from available water resources. Similar to water supply, agricultural, industrial, and domestic water withdrawal rates slow down when their demands approaching max water withdrawal rate. This process is represented by water withdrawal fulfillment rate ($$Wat\_Withd\_Fulf$$). Particularly for agricultural water withdrawal ($$Wat\_Withd\_Agri$$), impacts from extreme drought ($$Drght\_Rat$$) is also considered to simulate the decrease in $$Wat\_Withd\_Agri$$ and available water resources due to drought.

$$
Wat\_Withd\_Agri(t) = Wat\_Dem\_Agri(t) \times Wat\_Withd\_Fulf(t) \times (1-Drght\_Rat)
$$

(Eq. 4.4)

Agriculture, industrial, and domestic water withdrawal rates accumulate as total used water resources. As mentioned in the section **4.1 Water supply and water availability**, a fraction of total used water resources (set as 10%) can be recovered and supplied as available water resources.

## References
- 2030 Water Resources Group, 2009. Charting Our Water Future: Economic frameworks to inform decision-making.