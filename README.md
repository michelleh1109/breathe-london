# breathe-london
Research in Cornell Sibley School of Mechanical and Aerospace Engineering with Prof. K. Max Zhang; Developed algorithms to extract air pollution hotspot and source insights from distributed air quality sensor networl

### Introduction
Cities are investing into distributed air quality monitoring networks to combat PM2.5 emissions as exposure can lead to premature mortality, decreased quality of life, and cardiovascular problems. Alarmingly, 97% of global cities still fail to meet the WHO PM2.5 guidelines. Yet few studies investigate how to extract insight from these networks to develop pollution control measures. Especially with growing traffic-reduction initiatives in advanced cities, the proportion of non-traffic
related emissions is rising. It is vital to target these non-traffic sources to meet WHO health guidelines. Categorizing non-traffic emissions sources is difficult due to spatial-temporal variability, intermixing primary sources, and high transboundary and secondary formation sources,  
This research develops algorithms for cities to systematically extract hotspot and source identification from their distributed network. A major accomplishment is the identification of major non-traffic related sources at their site locations that have been previously challenging to characterize in the emission inventories. 

## Network Analysis
We identified fewer, but more accurate ”true” hotspots, which differs from conventional methods to capture a broad net of locations.  This optimizes limited resources to maximize impact.  The key principle of network analysis is to explore variability within the network to screen for PM2.5 hotspots against background concentrations. Intra-ranking algorithm first ranks sites between days to to filter out regional phenomena. Inter-ranking then ranks between monitoring sites’  daily PM2.5 concentrations ("inter”) on each day and is robust against outlier periods. However, 
our initial iterations were doing exactly what we didn’t want: identifying “false” hotspots with only slightly elevated PM2.5 concentrations, leading to months of inconclusive local investigation. A year in, I realized our conceptual flaw: inter-ranking treated all flagged days equally, regardless of their rankin g (i.e. sites in the top x% each day are binary flagged, and those with over y% flagged days in the study period are hotspots). I introduced a new weighted inter-ranking algorithm that prioritized sites consistently highly ranked instead of binary classification. 

## Peak Analysis Clustering Algorithm
The goal of clustering on air pollution is to group sites by their emissions patterns, which should be indicative of shared hyperlocal sources. 
However, initial clustering attempts on PM2.5 concentrations were unsuccessful. Strict emissions standards like the ULEZ congestion charge and transboundary sources from mainland Europe create high proportion of background concentrations that make hyperlocal sources difficult to isolate. In air pollution, peaks are also of interest because they can indicate hyperlocal emissions above backgrounds levels. I turned to peak analysis to identify local maxima in the time-series data. Initial iterations of peak analysis had many failed attempts including looking at: higher-dimensional relationships; weekly and seasonal peak patterns; clustering on the shape of peaks, etc. Finally, noticing the peaks displayed diurnal patterns, I merge previously unsuccessful iterations of peak analysis and clustering to develop the key achievement of this research. The peak analysis clustering algorithm categorizes of non-traffic and traffic related emissions sources. For each site, I apply peak analysis and calculate the frequency of peaks at every hour throughout the entire study period. Each site has a unique diurnal peak distribution. The diurnal patterns are then smoothed with kernel density estimates and clustered using k-means. Above, we can see traffic and non-traffic clusters. While 90% of sites were traffic driven, there were multiple smaller non-traffic clusters, indicating shared emission sources across the city. I investigated the non-traffic clusters containing hotspots as an indicator of major emissions activity. Local investigation revealed multiple sites of heavy construction activity and late-night commercial cooking that align with diurnal cluster patterns. Construction and cooking are the 3rd and 4th biggest PM2.5 sources in London only behind traffic and biomass burning, supporting the importance of our work in identifying these sources. As such, the synergy of hotspot identification and peak analysis clustering identified a construction cluster and commercial cooking cluster. This enables cities to target city-wide, non-traffic related PM2.5 emissions source beyond just network outliers. 
![image](https://github.com/michelleh1109/breathe-london/assets/90575654/a3177939-7735-4efd-86ad-e5bdff4bfdd6)










