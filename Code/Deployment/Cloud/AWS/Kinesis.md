# Kinesis

A family of services that enables you to collect, process, and analyze streaming data in real time

Allows you to build custom applications for your own business needs

Kinesis deals with data that is in motion, or streaming data

Streaming data
Data generated continuously by thousands of data sources that typically send in the data records simultaneously and in small sizes (kb).

- Financial transactions
- Stock prices
- Game data (as the player plays)
- Social media feeds
- Location-tracking data (Uber)
- IoT sensors
- Clickstream data
- Log files

Core services
- Kinesis streams
	- data
	- video
- Kinesis Data Firehose: capture, transform and load data streams into AWS data stores for real time analytics
- Kinesis data analytics: Analyze, query and transform streamed data in real time using standard SQL. Store the results in an AWS data store
	- Comes after firehose/streams to be able to query data

Kinesis shards
- Kinesis streams are made of shards
- Each shard is a sequence of one or more data records and provides a fixed unit of capacity
- Five reads / s
- Max total reads 2mb/s
- 1000 writes / s
- Max total writes is 1MB / s

The data capacity of the stream is determined by the number of shards.
If data rate increases, you can increase the number of shards


[Example CloudFormation](https://github.com/ACloudGuru-Resources/course-aws-certified-developer-associate/blob/main/Setting_Up_A_Kinesis_Data_Stream-Demo/kinesis-data-vis-sample-app.template)


---

