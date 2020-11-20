# Data Management and Algorithms for Big Data
~Sabrina Göllner, Izabela Burevska, Ahmad Khalidi, Olaf Zukunft (Prof)~

We are three students studying Master Computer Science at the HAW Hamburg. Our subject is Big Data and Data Science. For one project we have to implement a big data pipeline on a subject of our choice. This subject is the Corona-Virus. Our goal is to implement a pipeline where Tweets about health issues and official Corona-cases are being aggregated and then made available on a dashboard. For that we use technologies like Apache Spark, Docker and Python Notebook in a Lambda-Architecture. This project is a feasibility study and won’t be accessible by the general public.

## Dashboard
![Dashboard Mockup](/home/ahmad/Documents/Studium/Master/DAD/Projekt/Dashboard_Mockup.png  "Dashboard")

*Drawing 1: Dashboard* shows an example of such a Dashboard. It shows some hashes the user can filter tweets from. Filtering by area is also available. Any update on the filter updates all the other graphics. The interactive map shows appearances (in numbers) of any given tweet. The correlation timeline shows appearances over time and one may see correlations between tweets and official cases. The word-bubble (most used words) displays the most relevant words in those tweets. This drawing only illustrates a first mock up of our goal and may change in details.
## Architecture
We chose the Lambda-Architecture because it is well documented and suited for our study. Tweets are tweeted in a constant stream and an efficient computation of the view helps in efficiency and with future changes.
![Architecture](/home/ahmad/Documents/Studium/Master/DAD/Projekt/Application_Architecture.png  "Architecture")

*Drawing 2: Architecture* shows the architecture of the pipeline with all important steps. First we will request the Tweets over the Twitter API using filter like Hashes and Tweet- and Home-location. Next we save those tweets in a data lake, where those tweets are cleaned by using clustering algorithms so that only tweets with the given context are being processed. In The batch layer those objects will be form any needed View, where as in the Speed Layer the current Views are being expanded with newly incoming tweets. The Dashboard requests the data from the given Views and displays aggregated data.
## Deployment
All System components will be deployed on our personal computers. There will be no public access on the running system nor the finished dashboard. For a simple and independent deployment we are using docker-compose. Our current compose consist of a Spark-Network and Jupyter Lab described in this [GitHub](https://github.com/cluster-apps-on-docker/spark-standalone-cluster-on-docker).
## Pipeline Example for Interactive Map
As seen in  *Drawing 3: pipeline example*, we are using the given location either in the tweet itself or of the home location of the user to map the hashtags to the cities in the cleaning process (upper left box).
After transform the json into pyspark dataframe and group by (aggregate) over all citites and hashtags to get the count of all unique combinations. This process is done on the spark batch ecosystem.
The result is shown in an interactive map made with python folium library(based on open street maps). The map shows all upcoming tweets with given hashtags in given citites.
![Pipeline Example](/home/ahmad/Documents/Studium/Master/DAD/Projekt/Pipeline_Interactive_map.png  "Pipeline Example")
## Personal Data Protection
We have no intention of using those data on a personal level. That being said, we will make sure there will be no data displayed, so that one can trace back individuals and their symptoms. For example the interactive map shown in  *Drawing 1: Dashboard* will not be used on a fine-grained level. Bigger cities may be divided into districts or popular areas. Each individual of our group will apply if needed for their own access-token. We will also make sure to formally request any major changes if needed. We will share our results in a closed group of students and professor Olaf Zukunft.