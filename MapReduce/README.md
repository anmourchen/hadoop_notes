# Using Hadoop's Core: HDFS and MapReduce

We will use `mrjob==0.5.11` in `python` to run the MapReduce tasks. In the lecture, we will use `u.data` downloaded from `MovieLens-100k` dataset. It contains the `user_id`, `movie_id`, `ratings` and `timestamps`.

## Count the number of users for each rating score.
   
In this task, we want to find out the distributions for each rating score from 1-5.  

### Run locally
Use the following command to output the number of users for each rating socre locally without using hadoop.  

```
python RatingsBreakdown.py u.data
```

And it will give you the following output:

```
No configs found; falling back on auto-configuration
Creating temp directory /var/folders/71/nlvp2f555hv9qkqsxmcg3ngc0000gn/T/RatingsBreakdown.yanfeichen.20190622.015730.250280
Running step 1 of 1...
Streaming final output from /var/folders/71/nlvp2f555hv9qkqsxmcg3ngc0000gn/T/RatingsBreakdown.yanfeichen.20190622.015730.250280/output...
"5"	21203
"1"	6111
"2"	11370
"3"	27145
"4"	34174
Removing temp directory /var/folders/71/nlvp2f555hv9qkqsxmcg3ngc0000gn/T/RatingsBreakdown.yanfeichen.20190622.015730.250280...
```

For some reason, `rating` is not sorted based on `count` on my system.

### Run with Hadoop

You will need a server with hadoop installed to run the following command:

```
python RatingsBreakdown.py -r hadoop --hadoop-streaming-jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar u.data
```

`u.data` is located on our local file system, but it will be copied to `HDFS` system in real life.

## Sort the movie by number of rated users and find the most popular movie

In this task, we will need two ``MapReducer` steps, as shown in `SortMovieRatingCount.py`. Similarly, we can run locally or run with hadoop using the same commands.

### Run locally

Run the following command:

```
python MapReduce/SortMovieRatingCount.py ./MapReduce/u.data
```

And here is the output:

```
No configs found; falling back on auto-configuration
Creating temp directory /var/folders/71/nlvp2f555hv9qkqsxmcg3ngc0000gn/T/SortMovieRatingCount.yanfeichen.20190622.021519.741698
Running step 1 of 2...
Running step 2 of 2...
Streaming final output from /var/folders/71/nlvp2f555hv9qkqsxmcg3ngc0000gn/T/SortMovieRatingCount.yanfeichen.20190622.021519.741698/output...

(...)

"7"	"00392"
"56"	"00394"
"127"	"00413"
"174"	"00420"
"121"	"00429"
"300"	"00431"
"1"	"00452"
"288"	"00478"
"286"	"00481"
"294"	"00485"
"181"	"00507"
"100"	"00508"
"258"	"00509"
"50"	"00584"
```

For some reason, `movie_id` is not sorted based on `count` on my local system.

### Run with Hadoop

Use the same command.
