
### Summary of Session 2: Indexes and Data Onboarding

This session reviewed the topics from the previous day and then focused on understanding Splunk indexes and the process of onboarding data.

#### What are Splunk Indexes?

Indexes are the repositories where Splunk data is stored. When the Splunk platform processes raw data, it transforms that data into searchable events within an index. These indexes are stored as flat files directly on the indexer component.

There are two main types of indexes:
* **Events indexes**: This is the default index type and it can hold any kind of data.
* **Metrics indexes**: This type is used exclusively for metric data. Metric data is defined as having a numerical measurement, a metric type, and one or more dimensions.

---
#### Data Sources and Onboarding

Splunk is capable of ingesting data from many sources, such as files, directories, APIs, and network events. It supports several common data formats, including JSON, CSV, and XML, as well as custom formats.

The presentation outlined the steps to upload a data file through the Splunk user interface:
1.  First, you select a **sourcetype** for the data you are adding.
2.  You may need to resolve any errors that appear before clicking **Next**.
3.  You then select the specific **index** where you want to store the data from your file.
4.  Finally, you **Review** your settings and click **Submit** to complete the upload.

---
#### Removing Data

Data can be removed from Splunk by using the `| delete` command in the search bar. A note of caution was provided, stating that this is a very destructive command that should not be used without assistance.

---
