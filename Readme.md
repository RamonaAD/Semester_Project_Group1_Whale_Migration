# Proposal for Semester Project


<!-- 
Please render a pdf version of this Markdown document with the command below (in your bash terminal) and push this file to Github. 
Please do not Rename this file (Readme.md has a special meaning on GitHub).

quarto render Readme.md --to pdf
-->

**Patterns & Trends in Environmental Data / Computational Movement Analysis / Geo 880**

| Semester:      | FS26                                     |
|:---------------|:---------------------------------------- |
| **Data:**      | Satellite tag-derived animal movement data  |
| **Title:**     | Identifying migration pathways of Australia's east coast humpback whale breeding stock E1 using satellite tag-derived data                  |
| **Student 1:** | Ramona Adriana Davuke                        |
| **Student 2:** | Meret Schindler  |

## Abstract 
Humpback whales migrate annually between feeding and breeding grounds. Therefore, satellite tags were deployed on 50 humpback whales (*Megaptera novaeangliae*) between Australia and Antarctica between 2008 and 2010 during their movements in coastal breeding areas, along their northward and southward migration routes, and at their Antarctic feeding grounds. The aim of this project is to replicate the spatial and temporal patterns of humpback whale migration based on an existing study.

## Research Questions
The aim is to identify migratory pathways between Australia and Antarctica for breeding stock E1 humpback whales (Megaptera novaeangliae) using satellite-tag derived movement trajectories.  

•	Can migratory pathways of breeding stock E1 humpback whales be identified using satellite-tag derived movement data? 

•	Can seasonal patterns of these humpback whales be identified? 

•	Can humpback whale behavioural states be identified based on their location and speed? 

## Results / products
This project will generate various visualisations of the trajectories of breeding stock E1 humpback whales between Australia and Antarctica. Spatial and temporal patterns of humpback whale migration will be analysed by creating trajectory maps. To identify differences between individual humpback whales, a satellite deployment duration graphic will be generated. In addition, travel direction, speed, and behavioural state will be summarised in a table. 
Overall, this study will identify migration pathways of the humpback whale breeding stock E1 and analyse spatial and temporal patterns in their movements. This improves understanding of migration connectivity and provides a baseline for conservation strategies to reduce the risk of ship strikes and underwater noise. 


## Data
Movebank is an online database to manage, share, analyse or archive data for animal tracking (Movebank, 2026). For this study, two datasets provided by Andrew-Goff et al. (2023) will be downloaded as .csv data format from Movebank. The first dataset includes Metadata information about the tagged humpback whales and the individuals satellite tag deployment, while the second dataset displays the trajectory data between 2008 and 2011. Table 1 shows the attributes used for the analysis based on the data provided by Andrew-Goff et al. (2023). More information on the datasets can be accessed on https://datarepository.movebank.org/entities/datapackage/7fb8ee56-cb2d-4c4c-9456-166fc8e3ee6d. 

*Table 1: Table showing the attributes (Column label) used in this study and their descriptions*

| Column label | Description |
|:---------------|:---------------------------------------- |
| animal-id or individual-local-identifier | Unique animal identifier |
| deploy-on-date | Timestamp when tag deployment started |
| deploy-off-date | Timestamp when tag deployment ended |
| deploy-on-latitude | Geographic latitude location of deployment | 
| deploy-on-longitude | Geographic longitude location of deployment |
| duty cycle | Frequency of satellite tag transmissions, and times the transmitter is on or off | 
| timestamp | Time of satellite tag transmission. Format: yyyy-MM-dd HH:mm:ss:SSSS; Time zone: UTC | 
| argos:lat1 | Argos geographic latitude location estimates in decimal degrees. Reference system: WGS84 | 
| argos:lon1 | Argos geographic longitude location estimates in decimal degrees. Reference system: WGS84 | 
| argos:lc | Location classes as defined by the Argos User’s Manual (CLS, 2016) | 


## Analytical concepts
As humpback whales migrate annually between feeding and breeding grounds, their long-distance migration and seasonal pathways will be analysed within a movement ecology framework, particularly focusing on migration ecology and seasonal habitat use. Movement within a marine environment is conceptualised in a geodesic spatiotemporal space. Since trajectories are derived from Argos satellite-tags, a state-space model (SSM) will be used to reconstruct movement paths and account for location uncertainty. Subsequently, step length, travel speed, turning angle and direction will be derived using point-to-point movement modelling. Additionally, to identify changes in movement behaviour along migration pathways, track segmentation will be applied, allowing the distinction between behavioural states such as directed or localized movement. Lastly, a hotspot analysis using the Kernel density estimation (KDE) will be used to identify areas of concentrated use. 

## R concepts
The data analysis will be conducted using R Studio (R Core Team, 2025). To account for Argos location uncertainty a correlated random walk state-space model will be generated using the aniMotum package (fit_ssm function; Jonson et al., (2023). In addition, the algorithm based sdafilter function will be used to remove unlikely position estimates (sdafilter function in the argosfilter package; Freitas et al. 2008). Furthermore, step length, travel speed, and turning angle will be calculated using functions of the amt package (make_track and steps_by_burst functions; Signer et al., 2019). Travel direction will be determined using the geosphere package (bearing function; Hijmans, 2010). Next, trajectory maps will be created using tm_shape functions of the the tmap package (Tennekes, 2018). Segmentation analysis will be used to identify behavioural states (lead/lag functions from Wickham et al., 2019; st_distance function; Pebesma and Bivand, 2023). For KDE hotspot analysis, the spatstat.geom and spatstat.explore packages will be used applying as.ppp and density.ppp functions (Baddeley et al., 2013; Baddeley and Turner, 2005). 

## Risk analysis
Time constraints may be one of the main challenges in this study. The use of movement ecology methods and associated R packages (e.g. state-space model and Argos filtering) which are new to the authors requires initial time for familiarisation to ensure correct implementation. The Argos User’s Manual will be used as a guide. Yet, if more time than planned is required for the pre-processing step of state-space modelling and Argos filtering, speed and travel direction will not be analysed. In addition, creating suitable visualisations showing trajectories of 50 humpback whale individuals may be another obstacle. However, practical inputs from classes and the use of ChatGPT, a generative AI, can help the authors overcome this issue. 

## Questions? 
1. Shall we analyse step length, travel speed, turning angle, travel direction and behavioural state for all 50 individuals or choose a smaller sample (e.g. 10 individuals)?
2. Which exclusion criteria should we use for a smaller sample (e.g., tracking duration, year, sex, frequency of satellite tag transmissions, Argos location error etc)?
3. How should we consider the various classes of Argos location errors?  LC 3 has an estimated error of 250 m, LC 2 has an estimated error between 250 and 500 m and LC 1 has an estimated error between 500 and 1500 m. LC 0 has an open-ended error of 1500 m. LC A and B have no accuracy estimation and LC Z is an invalid location.
4. Should we exclude LC A and B and LC Z from the analysis? 
5. Is there something we need to consider due to geodesic spatiotemporal space? 
6. Is speed still a legitimate parameter to calculate? Whales do not only travel horizontally, but vertically. 

## References

Andrews-Goff, V., Gales, N., Childerhouse, S. J., Laverick, S. M., Polanowski, A. M., & Double, M. C. (2023). *Data from: Australia’s east coast humpback whales: satellite tag derived movements on breeding grounds, feeding grounds and along the northern and southern migration.* [Dataset]. Movebank Data Repository. https://doi.org/10.5441/001/1.294
Movebank. (n.d.). *Get started with Movebank.* Movebank. Retrieved May 3, 2026, from https://www.movebank.org/cms/movebank-content/get-started


