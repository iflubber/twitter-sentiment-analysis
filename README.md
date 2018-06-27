**Project2: **

**Sentiment Analysis using Social Media Data**

**Sentiment Data:**

Unstructured data on opinions, emotions and attitudes contained in
sources like social media, blogs, online product reviews and customer
support interactions

**Potential Uses of Sentiment Data**

Organizations use sentiment analysis to understand how the public feels
about something at a particular moment in time, and also to track how
those opinions change over time. An enterprise may analyze sentiment
about:

A product –For example, does the target segment understand and
appreciate messaging around a product launch? What products do visitors
tend to buy together, and what are they most likely to buy in the
future?

A service –For example, a hotel or restaurant can look into its
locations with particularly strong or poor service.

Competitors –In what areas do people see our company as better than (or
weaker than) our competition?

Reputation –What does the public really think about our company? Is our
reputation positive or negative?

In this project, we will focus on a product launch. Specifically, we
will look at public sentiment during the days leading up to and
immediately following the recent release of the movie Deadpool 2.

How did the public feel about the debut, and how might that sentiment
data have been used to better promote the movie’s launch?

**Input Data**

You can download a set of sample Twitter data contained in a compressed
(.zip) folder which was collected from one following way.

1\. The Twitter data was obtained using Flume. Flume can be used as a log
aggregator, collecting log data from many diverse sources and moving it
to a centralized data store. In this case, Flume was used to capture the
Twitter stream data, which we can now load into the Hadoop Distributed
File System (HFDS).

2\. We can also use R-Hadoop integration and connect R with Twitter to
extract the tweets data and upload as jsonfiles

3\. We can also collect the reviews from any other social media website
using WebCrawlers

**Expected Output:**

In order to optimize your website and convert more visits into sales and
revenue.

To refine and visualize website sentiment data, we will:

Download and extract the sentiment tutorial files.

Twitter data in a tabular format with sentiment ratings

How sentiment varies by country, and review the sentiment data for the
United States

***Solution:***

1\. Setting up raw data folders in **HDF**S and copy the dictionary files
and time\_zone\_map data

![](./screenshots/media/image1.tiff){width="6.263888888888889in"
height="1.3597222222222223in"}

![](./screenshots/media/image2.tiff){width="6.263888888888889in"
height="0.8222222222222222in"}

![](./screenshots/media/image3.tiff){width="6.263888888888889in"
height="0.8486111111111111in"}

2\. Extract Data from Twitter using **Flume**

**twitter.conf**

TwitterAgent.sources = Twitter

TwitterAgent.channels = MemChannel

TwitterAgent.sinks = HDFS

\# Describe & configure the source

\# TwitterAgent.sources.Twitter.type =
org.apache.flume.source.twitter.TwitterSource

TwitterAgent.sources.Twitter.type =
com.cloudera.flume.source.TwitterSource

TwitterAgent.sources.Twitter.channels = MemChannel

TwitterAgent.sources.Twitter.consumerKey = XXXXXXXXXXXXXXXXXX

TwitterAgent.sources.Twitter.consumerSecret = XXXXXXXXXXXXXXXXX

TwitterAgent.sources.Twitter.accessToken = XXXXXXXXXXXXXXXXX

TwitterAgent.sources.Twitter.accessTokenSecret = XXXXXXXXXXXXXX

TwitterAgent.sources.Twitter.maxBatchSize =1000

TwitterAgent.sources.Twitter.keywords = deadpool

\# Describe & configure the sink

TwitterAgent.sinks.HDFS.channel = MemChannel

TwitterAgent.sinks.HDFS.type = hdfs

TwitterAgent.sinks.HDFS.hdfs.useLocalTimeStamp = true

TwitterAgent.sinks.HDFS.hdfs.path = /user/cloudera/data/tweets\_raw

TwitterAgent.sinks.HDFS.hdfs.fileType = DataStream

TwitterAgent.sinks.HDFS.hdfs.writeFormat = Text

TwitterAgent.sinks.HDFS.hdfs.batchSize = 10

TwitterAgent.sinks.HDFS.hdfs.rollSize = 0

TwitterAgent.sinks.HDFS.hdfs.rollCount = 10000

TwitterAgent.sinks.HDFS.hdfs.rollInterval = 600

\# Use a channel which buffers events in memory

TwitterAgent.channels.MemChannel.type = memory

TwitterAgent.channels.MemChannel.capacity = 10000

TwitterAgent.channels.MemChannel.transactionCapacity = 1000

![](./screenshots/media/image4.tiff){width="6.263888888888889in"
height="0.6695658355205599in"}

![](./screenshots/media/image5.tiff){width="6.263888888888889in"
height="2.90625in"}

![](./screenshots/media/image6.tiff){width="6.263888888888889in"
height="0.6604166666666667in"}

3\. Import data into **Hive** and perform analysis

![](./screenshots/media/image7.tiff){width="6.263888888888889in"
height="0.8076388888888889in"}

**Import Data**

![](./screenshots/media/image8.tiff){width="6.263194444444444in"
height="2.765217629046369in"}

![](./screenshots/media/image9.tiff){width="6.263888888888889in"
height="5.4875in"}

![](./screenshots/media/image10.tiff){width="6.263888888888889in"
height="3.1819444444444445in"}

![](./screenshots/media/image11.tiff){width="6.263888888888889in"
height="3.222916666666667in"}

Prepare for Analysis

![](./screenshots/media/image12.tiff){width="6.263888888888889in"
height="2.122916666666667in"}

![](./screenshots/media/image13.tiff){width="6.263888888888889in"
height="2.548611111111111in"}

![](./screenshots/media/image14.tiff){width="6.263888888888889in"
height="1.8090277777777777in"}

![](./screenshots/media/image15.tiff){width="6.263888888888889in"
height="2.314583333333333in"}

![](./screenshots/media/image16.tiff){width="6.263888888888889in"
height="3.65625in"}

![](./screenshots/media/image17.tiff){width="6.263888888888889in"
height="3.9569444444444444in"}

![](./screenshots/media/image18.tiff){width="6.263888888888889in"
height="2.6956528871391074in"}

![](./screenshots/media/image19.tiff){width="6.208333333333333in"
height="2.7826082677165354in"}

![](./screenshots/media/image20.tiff){width="6.263888888888889in"
height="1.7854166666666667in"}

**Perform Analysis**

10 most common hashtags

![](./screenshots/media/image21.tiff){width="6.263888888888889in"
height="6.525in"}

Country-wise sentiments

![](./screenshots/media/image22.tiff){width="6.263888888888889in"
height="4.152777777777778in"}

Top 10 countries generating positive sentiments

![](./screenshots/media/image23.tiff){width="6.263888888888889in"
height="4.159027777777778in"}

Top 10 countries generating negative sentiments

![](./screenshots/media/image24.tiff){width="6.263888888888889in"
height="4.263194444444444in"}

Sentiment mix:

![](./screenshots/media/image25.tiff){width="6.263888888888889in"
height="2.6222222222222222in"}

This shows the movie has received positive sentiments in majority which
is a good sign and probably is the indication that the promotional
activities are working in favour.

10 positive tweets:

![](./screenshots/media/image26.tiff){width="6.263888888888889in"
height="4.354861111111111in"}

10 negative tweets

![](./screenshots/media/image27.tiff){width="6.263888888888889in"
height="4.353472222222222in"}

Twitter users generating positive sentiment

![](./screenshots/media/image28.tiff){width="6.2625in" height="4.4in"}

List of Twitter users tweeting about ‘deadpool 2’

![](./screenshots/media/image29.tiff){width="6.263888888888889in"
height="3.4583333333333335in"}

List of Twitter users tweeting negatively about ‘deadpool’

![](./screenshots/media/image30.tiff){width="6.26248031496063in"
height="5.208695319335083in"}
