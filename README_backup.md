# Real-time sentiment analysis on Tweets

## Instructions to run

1. Set up access to pull Tweets from the Twitter API.
    a. Get a Twitter Developer account (https://developer.twitter.com/en).
    b. Create a "config.ini" file in the same directory as the rest of the files. Input the developer keys provided by Twitter without quotes.
        ```
        [twitter]

        api_key = XXX
        api_key_secret = XXX

        access_token = XXX
        access_token_secret = XXX
        ```
2. Start Docker.
3. In a command console, input `docker-compose up -d`.
4. Start the Kafka consumer with `docker exec spark-master bash scripts/start_consumer.sh` in the same command console. Wait until the command console ahst stopped producing logs. (may need to install the vadersentiment package https://anaconda.org/conda-forge/vadersentiment).
5. Start the Kafka producer in a separate command console with `python twitterProducer.py`.
6. Send data to InfluxDB by running `python toInfluxDF.py` in a third command console. (May need to install the influxdb-client package https://anaconda.org/conda-forge/influxdb-client).
7. View the results in the dashboard.
    a. Open InfluxDB in a browser from Docker.
    b. Sign in with credentials admin; admin123
    c. Select the Explore tab on the left.
    d. Select from the twitter_data>tag>score>sentiment. Select all tags you wish to view.
    e. On the right side, change "Past 1h" to a shorter timeframe to view the results ("Past 5m" suggested). Nothing will show if data is not consinuously fed into InfluxDB.


## How each file works
