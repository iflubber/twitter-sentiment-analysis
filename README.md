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

![](./screenshots/media/image1.tiff)

![](./screenshots/media/image2.tiff)

![](./screenshots/media/image3.tiff)

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

![](./screenshots/media/image4.tiff)

![](./screenshots/media/image5.tiff)

![](./screenshots/media/image6.tiff)

3\. Import data into **Hive** and perform analysis

![](./screenshots/media/image7.tiff)

**Import Data**

![](./screenshots/media/image8.tiff)

![](./screenshots/media/image9.tiff)

![](./screenshots/media/image10.tiff)

![](./screenshots/media/image11.tiff)

Prepare for Analysis

![](./screenshots/media/image12.tiff)

![](./screenshots/media/image13.tiff)

![](./screenshots/media/image14.tiff)

![](./screenshots/media/image15.tiff)

![](./screenshots/media/image16.tiff)

![](./screenshots/media/image17.tiff)

![](./screenshots/media/image18.tiff)

![](./screenshots/media/image19.tiff)

![](./screenshots/media/image20.tiff)

**Perform Analysis**

10 most common hashtags

![](./screenshots/media/image21.tiff)

Country-wise sentiments

![](./screenshots/media/image22.tiff)

Top 10 countries generating positive sentiments

![](./screenshots/media/image23.tiff)

Top 10 countries generating negative sentiments

![](./screenshots/media/image24.tiff)

Sentiment mix:

![](./screenshots/media/image25.tiff)

This shows the movie has received positive sentiments in majority which
is a good sign and probably is the indication that the promotional
activities are working in favour.

10 positive tweets:

![](./screenshots/media/image26.tiff)

10 negative tweets

![](./screenshots/media/image27.tiff)

Twitter users generating positive sentiment

![](./screenshots/media/image28.tiff)

List of Twitter users tweeting about ‘deadpool 2’

![](./screenshots/media/image29.tiff)

List of Twitter users tweeting negatively about ‘deadpool’

![](./screenshots/media/image30.tiff)
