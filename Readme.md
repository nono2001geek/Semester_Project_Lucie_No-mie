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
This project analyzes the alignment between the theoretical concept of the "15-minute city" and the actual mobility of an individual in Zurich. By superimposing precise GPS trajectories onto a modeling of services accessible within 15 minutes (walking/transit), we evaluate whether existing infrastructure dictates movement or if other factors prevail. The study aims to quantify the gap between the potential accessibility offered by Zurich's efficient transport model and actual mobility choices.

## Research Questions
<!-- (50-60 words) -->
1. How does the overlap between actual mobility and the 15-minute radius differ when comparing walking accessibility versus public transport accessibility?
2. Which types of activities (work, leisure, shopping) are systematically performed outside the accessible 15-minute radius, and why?
3. How does actual mobility behavior differ from the theoretical accessibility provided by public transport and road infrastructure?

## Results / products
<!-- (50-100 words) -->
<!-- What do you expect, anticipate? -->
We anticipate producing heatmaps comparing frequented zones against areas accessible within 15 minutes. The primary output will be a quantitative metric of the "mobility deficit": the percentage of trips made beyond the theoretical radius despite the availability of nearby services. We expect to reveal that, despite the excellence of Zurich's public transport network (tram, bus, S-Bahn), social or professional habits drive the individual to regularly exceed this optimal radius.

## Data
<!-- (100-150 words) -->
<!-- What data will you use? Will you require additional context data? Where do you get this data from? Do you already have all the data? -->
We will use a dataset of individual GPS traces (collected), containing latitude, longitude, timestamp, and potentially transport mode. For spatial context, we will integrate OpenStreetMap (OSM) data via API or geographic extracts, specifically for Zurich (city). This data will include Points of Interest (POI): schools, shops, parks, workplace, as well as the public transport network (VBZ tram stops, ZVV S-Bahn stations). Combining these sources will allow us to model dynamic isochrones (areas accessible within 15 min) based on the time of day.

## Analytical concepts
<!-- (100-200 words) -->
<!-- Which analytical concepts will you use? What conceptual movement spaces and respective modelling approaches of trajectories will you be using? What additional spatial analysis methods will you be using? -->
This project combines concepts from movement analysis and urban accessibility. Trajectory reconstruction will rebuild the individual’s movements from Google Timeline GPS data, while segmentation methods will distinguish trips, stops, and activities. Map matching will align GPS traces with Zurich’s street and public transport networks, and travel mode detection will identify whether movement occurred by walking, tram, train, or bicycle. Semantic annotation will classify destinations and activities such as work, shopping, or leisure.
The main conceptual movement spaces are the activity space and the space-time prism. The activity space represents the areas regularly used by the individual and will be analysed through trajectories, clustering, and heatmaps to identify recurring mobility patterns. The space-time prism represents the theoretical 15-minute accessible area and will be modelled using accessibility and network analysis based on realistic walking and public transport travel times.
Additional analyses include comparing actual and theoretical accessibility and calculating a mobility deficit metric quantifying trips beyond the accessible 15-minute radius.

## R concepts
<!-- (50-100 words) -->
<!-- Which R concepts, functions, packages will you mainly use. What additional spatial analysis methods will you be using? -->
The analysis will mainly use the R packages R, sf, dplyr, ggplot2, and tmap for spatial and mobility analysis. GPS data from Google Timeline will be converted into sf objects using st_as_sf() and projected with st_transform() to allow accurate distance calculations. Functions such as filter(), group_by(), mutate(), lead(), lag(), and difftime() will be used to reconstruct trajectories, calculate travel times, speeds, and identify trips or stationary activities. st_distance() will measure distances between locations and accessibility zones, while segmentation and static point detection methods will separate stops and movements. Finally, st_convex_hull() will estimate the individual’s activity space, and ggplot2/tmap will visualize trajectories, heatmaps, and accessibility overlaps.

## Risk analysis
<!-- (100-150 words) -->
<!-- What could be the biggest challenges/problems you might face? What is your plan B? -->
The major challenge lies in the precision and continuity of GPS data: signal loss or low sampling frequency could skew the calculation of transport modes and actual travel times. Furthermore, precise modeling of Zurich's public transport isochrones requires complex schedule data (GTFS) which can be computationally heavy. Plan B: If real-time public transport data is too complex to integrate, we will base isochrones on constant average speeds for trams and buses (e.g., 15 km/h) to approximate accessibility. If GPS data is too noisy, we will apply more aggressive smoothing algorithms or focus the analysis on significant stopping points rather than trajectory continuity.

## Questions? 
<!-- (100-150 words) -->
<!-- Which questions would you like to discuss at the coaching session? -->
1. Regarding accessibility modeling: is it analytically valuable to compute dual isochrones (15 minutes by foot vs. 15 minutes by public transport) to distinguish between "neighborhood" needs and metropolitan accessibility, or should we prioritize one mode? 
2. Our subject’s data includes significant travel outside Zurich; should we attempt to gather context data for these extra-urban locations, or is it more rigorous to classify them simply as "out-of-scope" mobility to maintain focus on the city model? 
3. Given incomplete GPS data (signal loss, battery saving), what interpolation thresholds do you recommend for bridging short gaps without introducing bias, and how should we formally label longer untracked periods in our trajectory analysis?
