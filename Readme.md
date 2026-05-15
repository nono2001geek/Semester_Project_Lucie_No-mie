# Proposal for Semester Project


<!-- 
Please render a pdf version of this Markdown document with the command below (in your bash terminal) and push this file to Github. 
Please do not Rename this file (Readme.md has a special meaning on GitHub).

quarto render Readme.md --to pdf
-->

**Patterns & Trends in Environmental Data / Computational Movement Analysis / Geo 880**

| Semester:      | FS26                                     |
|:---------------|:---------------------------------------- |
| **Data:**      | Individual GPS Trajectories (high frequency) & POI (Points of Interest) / Infrastructure Data for Zurich  |
| **Title:**     | The 15-Minute City in Practice: Comparing Theoretical Accessibility and Actual Mobility Behavior in Zurich |
| **Student 1:** | Lucie Kern                        |
| **Student 2:** | Noémie Simon                        |

## Abstract 
<!-- (50-60 words) -->
This project evaluates the extent to which Zurich aligns with the "15-minute city" concept by comparing theoretical accessibility to actual mobility behavior of an individual in living in Zurich. Using Google Timeline movement data and accessibility modelling of services within 15 minutes, the study quantifies mismatches between nearby available services and daily travel patterns, examining whether mobility is primarily shaped by infrastructure.

## Research Questions
<!-- (50-60 words) -->
1. What proportion of an individual’s daily activities in Zurich occurs within 15 minutes from home, walking, cycling, or by public transport? 
2. How does actual mobility behavior differ from the theoretical accessibility provided by services and infrastructure? 
3. Which types of activities (work, entertainment, groceries, sport, leisure, social visits) most frequently occur beyond a 15‑minute travel time from home?

## Results / products
<!-- (50-100 words) -->
<!-- What do you expect, anticipate? -->
We will map the 15-minute accessibility areas and the most frequently visited locations, in addition we will provide quantitative indicators showing the proportion of activities occurring within or outside theoretically accessible 15-minute areas, differentiated by transport mode and activity type. Results will compare theoretical accessibility with actual destinations, classify local versus non-local activities, and visualize mobility patterns through heatmaps of visited locations. We expect to show that, despite Zurich’s highly efficient public transport network, social and professional habits regularly lead individuals to exceed the 15-minute radius, demonstrating that accessibility alone does not determine mobility behavior.

## Data
<!-- (100-150 words) -->
<!-- What data will you use? Will you require additional context data? Where do you get this data from? Do you already have all the data? -->
We will use a dataset of individual movement data collected through google timeline over 3 months, containing latitude, longitude, timestamp and transport mode. To ensure privacy, all personally identifiable information, including the exact home location, will be anonymized and spatially generalized before analysis. For spatial context, we will integrate OpenStreetMap (OSM) data via API or geographic extracts, specifically for Zurich (city). This data will include Points of Interest (POI): schools, shops, parks, workplace, as well as the public transport network (VBZ tram stops, ZVV S-Bahn stations). Combining these sources will allow us to model dynamic isochrones (areas accessible within 15 min) based on the time of day.

## Analytical concepts
<!-- (100-200 words) -->
<!-- Which analytical concepts will you use? What conceptual movement spaces and respective modelling approaches of trajectories will you be using? What additional spatial analysis methods will you be using? -->
This project combines concepts from movement analysis and urban accessibility. Trajectory reconstruction will rebuild the individual’s movements from Google Timeline GPS data, while segmentation methods will distinguish trips, stops, and activities. Map matching will align GPS traces with Zurich’s street and public transport networks, and travel mode detection will identify whether movement occurred by walking, tram, train, or bicycle. Semantic annotation will classify destinations and activities such as work, shopping, or leisure.
The main conceptual movement spaces are the activity space and the space-time prism. The activity space represents the areas regularly used by the individual and will be analysed through trajectories, clustering, and heatmaps to identify recurring mobility patterns. The space-time prism represents the theoretical 15-minute accessible area and will be modelled using accessibility and network analysis based on realistic walking and public transport travel times.
Additional analyses include comparing actual and theoretical accessibility and calculating a mobility deficit metric quantifying trips beyond the accessible 15-minute radius.

## R concepts
<!-- (50-100 words) -->
<!-- Which R concepts, functions, packages will you mainly use. What additional spatial analysis methods will you be using? -->
The following R packages will be used: jsonlite, lubridate, tidyverse, sf, dplyr, ggplot2, and tmap for spatial and mobility analysis. GPS data from Google Timeline will be converted into sf objects using st_as_sf() and projected with st_transform() to allow accurate distance calculations. Functions such as filter(), group_by(), mutate(), lead(), lag(), and difftime() will be used to reconstruct trajectories, calculate travel times, speeds, and identify trips or stationary activities. st_distance() will measure distances between locations and accessibility zones, while segmentation and static point detection methods will separate stops and movements. Finally, st_convex_hull() will estimate the individual’s activity space, and ggplot2/tmap will visualize trajectories, heatmaps, and accessibility overlaps.

## Risk analysis
<!-- (100-150 words) -->
<!-- What could be the biggest challenges/problems you might face? What is your plan B? -->
The major challenge lies in the precision and continuity of GPS data: signal loss or low sampling frequency could skew the calculation of transport modes and actual travel times. Furthermore, precise modeling of Zurich's public transport isochrones requires complex schedule data (GTFS) which can be computationally heavy. Plan B: If real-time public transport data is too complex to integrate, we will base isochrones on constant average speeds for trams and buses (e.g., 15 km/h) to approximate accessibility. If GPS data is too noisy, we will apply smoothing algorithms or filter our data.
Another challenge is to include all the services that are accessible within the radius. If there is no satisfactory data on that, a plan B would be to focus on mobility infrastructure rather than points of interest and replace the 2n research question by "How is an individual’s observed mobility behavior in Zurich related to the travel times implied by the local transport and street network?"

## Questions? 
<!-- (100-150 words) -->
<!-- Which questions would you like to discuss at the coaching session? -->
1. Our 2nd research question implies we would include all services within the 15 minutes radius. Is OpenStreetMap (OSM) appropriate for that and for the scope of the project ? Since our transport data includes trips outside the Zurich area, would it be necessary to incorporate more detailed information for these other visited locations?
2. Regarding accessibility modeling: is it valuable to compute it 15 min radius per mode of transportation ? or should we simplify ? 
3. What is the best and most defensible way to classify activities?  is it by assigning the right category manually ? if yes, how do we document it ? or can we apply some sort of logic and algorithm ?
4. How can we correct wrong mode of transportation in raw data?
# 
