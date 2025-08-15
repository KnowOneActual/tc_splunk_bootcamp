

### Summary of Introduction to Splunk (Session 1)

#### What is Splunk?
Splunk is a software platform designed to search, analyze, and visualize machine-generated data from a variety of sources, including websites, applications, and other IT infrastructure components. It is capable of handling unstructured, semi-structured, and structured data. After ingesting data, Splunk allows users to search it, create tags, and build reports and dashboards. It is also utilized for big data analysis.

***

#### Splunk Product Categories
Splunk is available in three main versions:
* **Splunk Enterprise**: Intended for companies with large IT environments, it gathers and analyzes data from sources like websites, applications, and sensors.
* **Splunk Cloud**: A cloud-hosted platform that offers the same features as the Enterprise version. It can be accessed directly from Splunk or via the AWS cloud.
* **Splunk Light**: A version with limited features that allows for real-time searching, reporting, and alerting on log data from a single location.

***

#### Key Features
Splunk's core functionality includes:
* **Data Ingestion**: It can ingest many data formats, such as JSON, XML, and unstructured machine data like application logs. This data can then be modeled into a user-defined structure.
* **Data Indexing**: Ingested data is indexed to facilitate faster searching and querying.
* **Data Searching**: The search feature uses indexed data to create metrics, identify patterns, and predict trends.
* **Alerts**: Users can set up alerts to trigger emails or RSS feeds when specific data criteria are met.
* **Dashboards**: Search results can be visualized using charts, reports, and other pivot views in dashboards.

***

#### Core Components
A Splunk deployment consists of several key components:
* **Indexer**: This component processes and stores data from both local and remote sources.
* **Search Head**: A Splunk instance that manages search operations by distributing them to indexers and then consolidating the results.
* **Forwarder**: A lightweight Splunk instance that collects data from sources and forwards it to an indexer for processing and storage.
* **Deployment Server**: An instance that manages and distributes configurations, apps, and content to other Splunk components like forwarders and indexers.

***

#### Installation and User Management
The session provided a brief overview of installing Splunk Enterprise on Ubuntu using `wget` and `dpkg` commands. It also covered basic user management, detailing the steps to create a new user, assign roles, and set a default application through the "Settings > Users" menu in the Web UI.

***

#### Default Network Ports
Key default ports for Splunk Enterprise include:
* **9997**: Splunk-to-Splunk data forwarding.
* **8000**: Splunk Web UI.
* **8089**: API access.
* **8088**: HTTP Event Collector.