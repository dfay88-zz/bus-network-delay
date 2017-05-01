## Network Based Approach to Predicting Bus Delay
Daniel Fay, Felipe Gonzalez, Achilles Saxby
Center for Urban Science and Progress
New York University


### Problem Statement
The primary objective of this project was to develop a model to predict the status of a bus line, i.e., significantly early, early, on-time, delay, and significant delay. Currently, most techniques aimed at relieving network delay are corrective rather than preventative. By providing transit operators with a tool to predict the vulnerability of a network component given some time lag, preventative fleet management operations can be implemented to help reduce the overall delay to the network. We evaluate many different network, temporal and spatial features in order to identify which features are most significant to predicting delay. We compare  several different classification machine learning model’s performances and results, including logistic regression, naive bayes, bayesian networks, decision trees, and random forests. 

### Data and Processing
We used the MTA’s dataset that contains the MTA Bus Time Data from August 1, 2014 through October 31, 2014. Each record in the data set contains, for a single bus, the time of observation, bus location, bus route, next stop, distance from that stop, and other variables described below.
We selected some of the buses and grouped the data in time periods of hours based on the common groups used in literature for transit analysis (morning and afternoon peaks, etc). Secondly, we calculate whether each bus had and inbound or outbound direction. Finally for each bus, direction and time period we calculated the mean of the trip in minutes. Based on that, we came up with the delay label for our dataset using the following criteria:  
Less than 5 minutes below the mean: Early
Between 5 minutes below the mean and 5 minutes after the mean: On time
Between 5 and 15 minutes after the mean: Delay
After 15 minutes after the mean: Significant delay


#### Temporal Features
The temporal features considered for this analysis included the month, day of week, time period and hour. The time period was classified based on typical traffic conditions, i.e., peak AM, mid-day, peak PM and night. The granularity of the different model’s predictions were either hour or time period depending on the complexity of the machine learning model. 

#### Weather Features
The weather features used for this analysis were gathered using weather underground’s API. We hypothesized conditions, humidity, precipitation, temperature, visibility, and wind speed could be a significant factor when predicting bus delay. The weather data was gathered hourly for the entire year of 2016. 

#### Network Features
Two network features were calculated for this analysis - previous trip ratio and network delay state. Previous trip ratio describes the ratio of a previous bus trips travel time and the average travel time under those conditions, i.e., same bus line, direction, month, day of week and time period. The methodology behind this feature is that a recently completed trip would be a strong indicator of the next bus travel time. In order to allow adequate time lag between trips, the second most recent trip was used to calculate the ratio. 

Network delay state describes the overall network delay at a time t. The network delay states are calculated by creating a matrix of all bus line delay at every time t. Then using this matrix, the typical network delay states are calculated by clustering delay states at time t using K-means clustering. This clusters similar delay states at different times together in order to understand the most common delay states the network experiences over the year. To identify the optimal number of clusters a plot of the number of clusters and the total sum of squared errors within the cluster is evaluated. Based on the below plot, 6 clusters were identified as the optimal number of clusters. This was based on the fact that the sum of squared errors does not decrease substantially after 6 clusters. 
