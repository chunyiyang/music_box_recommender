# music_box_recommender


# Data Processing Steps
Raw data downloading: load_data.ipynb
Unzip and combine all log files to one: unpack_and_clean_files.sh
Create recommendation system model: recommender_system.ipynb

# Create recommendation system
•	Use spark-2.2.1-bin-hadoop2.7
from pyspark.sql import SparkSession
from pyspark.sql.functions import col, when, round, sum, avg
from pyspark.ml.evaluation import RegressionEvaluator
from pyspark.ml.recommendation import ALS

# Details 
1 Extract user_id, song_id, play_length, song_length, paid 5 columns from original data

2 Filter out null values

3 For same song_id, using max song length to replace song_length = ‘0’

4 For each user_id, check how many different songs played. Based on this information, categorize as active user or inactive user.

5 Calculate the most popular songs: songs that have been played by most users.

6 Use to calculate plaround(play_time / song_length) y times for one play record.

7 Use count(play_times) group by user_id, song_id, we can get rating information.

8 Use recommendForAllUsers from ALS from pyspark.ml.recommendation to create recommendation model.

9 Use most popular songs for inactive users.
