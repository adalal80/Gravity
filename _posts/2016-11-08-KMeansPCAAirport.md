---
layout: post
title: "KMeans++ Cluster Analysis using PCA on Airport Delays"
---

## KMeans++ Cluster Analysis using PCA on Airport Delays

This analysis investigates operations of major airports around the country to understand the characteristics of departure and operational delays:
- A certain degree of delay is expected in airport operations, however the FAA is noticing significant delays with certain airports
- When a flight takes off, it's departure delay is recorded in minutes, as well as operational data relating to this delay
- At the end of the year, this data is averaged out for each airport. Your datasets have these averaged for a 10 year range between 2004 and 2014
- Over this 10 year range, some delay times have not improved or have worsened.

The Jupyter Notebook associated with this blog, can be found [here.](https://github.com/adalal80/GA-DSI/blob/master/projects/projects-weekly/project-07/starter-code/project7-starter.ipynb)

#### Hypothesis:
Taxi Out time (time it takes to leave the airport from gate) is associate with congestion time. The number of flights in and out of the airport would cause the taxi out time to increase as the number of runways is limited. This will play a huge factor in departure delays. The variation between clusters should highlight the importance of this feature.

### The Dataset
1) Airport
List of attributes per each airport

2) Cancelations
Cancelation dataset list cancelations and diversion per each year from 2004 to 2014

3) Operations
Operations dataset lists delays, departures, arrivals and other operational metrics

### Assumptions and Risks
1) Use Diversions and Cancellations as a proxy for weather.

2) Taxi out time is a factor of number of flights and runways, such that a higher ratio of number of flights/runways will increase taxi out time.

3) FAA regions will be used to separate airports.

4) Not able to determine if weather caused departures.

5) Not able to weed out the % are due to mechanical failures, as gate departure delays could be due to late arrivals and weather.

### Exploratory Data Analysis & Visualizations

Two categorical variables created, based on the hub and spoke model of airports. Major hubs, secondary hubs, and spokes for 'ap_class'. FAA region class was created giving a number to each region. Airports were averaged over the years in the data, as there will be an airport in multiple clusters when doing the analysis. Analyzing the correlations between the features, there was multi-collinearity among many of the features. PCA will need to be conducted to reduce dimensionality.

Departures vs Delays(min)
![DepDelays](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project7/DepDelays.png?raw=true)

Percent on-time gate arrivals vs percent on-time gate departures
![gatearrivaldep](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project7/gate_arrival_departures.png?raw=true)

Departures vs Average Airport Departure Delays
![DepvsDelays](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project7/DeparturesvsDelays.png?raw=true)

Taxi Out Time vs Taxi Out Delay
![taxi_out_delay](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project7/taxi_out_delay.png?raw=true)

Average Gate Arrival vs Departure Arrival Delay
![arrival_dep_delay](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project7/arrival_dep_delay.png?raw=true)

#### Features to Consider

1. FAA Region Dummies: There might be similarities in terms of air traffic flow, such as new york area airports, or north east in general

2. Percent on-time gate departures, airport departures, gate arrivals: These are all percentages, this details the metrics for airport in terms of percentages of flights

3. Average gate departure delay, taxi out delay, airport delay, taxi-in delay, average block delay, gate arrival delay. These are all the associated delays

4. Taxi out time: Taxi out time should be a ratio of number of flights and number of runways. High flight/runway ratio, would mean longer lines to take off.

Not Considering
1. Departures, Approvals: This is the highest varied features, which resulted in the class labels following the number of departures.
2. Diversions/Cancellations: Any diversions and cancellations should not affect Delay, as it has not left/arrived at the airport


### PCA - Principal Component Analysis

Using the features listed in the previous sections, PCA was performed using Robust Scalar to scale the data. From the Explained Variance Ratio, the number of components/features will be set to 2. 

Explained Variance Ratio
![Explained_Var_ratio](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project7/ExplainedVarianceRatio.png?raw=true)

Using Distortion
![Distortion](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project7/Distortion_Kmeans.png?raw=true)

Using numer of components = 2, the KMeans++ cluster model gives the following clusters:
![KMeans_PCA](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project7/KMeans_PCA.png?raw=true)

The silhouette score for 8 clusters was 0.39. While that may not be high, it provided the best clusters in terms of groupings. The best silhouette score was 0.54, which was for 2 clusters. 

Performing a groupby on the cluster labels, using average of all the airports, gives us the following:
![XCluster_results](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project7/Xcluster_result.png?raw=true)

Analyzing these results, shows how each cluster varies in each column. For example, clusters 2 and 4, show approximately the same percent columns, but the only difference taxi out time.  Another example would be clusters 1 and 7, show that percent on-time gate departures and arrivals are equivalent, but percent on-time airport departures and avg taxi out time are different.

Using 3 Principal Components gives us the following 3D graph:
![3D](https://github.com/adalal80/adalal80.github.io/blob/master/images/Project7/3D.png?raw=true)

### Conclusion
The operational features are most correlated with delays are taxi out time (how long it takes from gate departure to take off), size and proximity of airports (more frequency of flights generally the more congested), and of course the the arrival of the plane. If the plane arrives late, the turnoaround time for offboarding, re-fueling, and on-boarding will be the same regardless of when it comes. Thus, if the plane arrives late, it will lead to departing late. Weather related data isn't known, but could use a proxy for departure cancellations and arrival diversions.

Airport's Next Steps should be ensuring the following:

1) Ensuring that proper equipment for weather is accessible, such as de-icing, snow plow etc...

2) If frequency of flights/runways is high, thus causing long taxi delays, cost-benefit analysis on building another runway.

3) Increase gate fees associated to airlines, thus only the more profitable companies can fly in/out. This should reduce number of flights. This would be similar to a usage tax.

4) Ask airlines to increase the flight time to incorporate the average delays.

