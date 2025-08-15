

### Summary of Session 4: Configuration & Data Handling

This session focused on the core concepts of how Splunk processes data, the different ways to deploy Splunk, and a deeper dive into using SPL for searching and transforming data.

***

#### How Splunk Handles Data

Splunk processes data in four key stages:

1.  **Data Input**: Splunk is configured to monitor specific data sources, like files or network ports.
2.  **Data Parsing**: Raw, unstructured data is converted into a structured format, making it searchable.
3.  **Data Indexing**: The parsed data is written to disk, creating an index for efficient searching.
4.  **Data Searching**: Users interact with the indexed data using the Search Processing Language (SPL).

***

#### Splunk Deployment Architectures

The session covered three main deployment types:

1.  **Standalone Deployment**: A single Splunk instance handles all four data stages. It's simple and good for learning but lacks high availability.
2.  **Distributed Deployment**: The roles are split across different servers: Forwarders handle data input, Indexers handle parsing and storage, and a Search Head handles searching.
3.  **Clustered Deployment**: The standard for production environments, this model adds redundancy and high availability with Indexer Clusters and Search Head Clusters to prevent data loss and handle many users.

The choice of deployment depends on factors like **indexing volume**, the **number of users**, and requirements for **high availability** and **disaster recovery**.

***

#### Searching and Filtering in Splunk

To search effectively, you need to know the correct **index** and **time range**. Splunk has custom indexes you create and default indexes for internal data, like `_internal` (Splunk's own logs) and `_audit` (login/logout logs).

You can filter data by adding keywords to your search or by selecting values from the fields Splunk automatically extracts.

***

#### Transforming Commands in SPL

The session introduced several powerful commands to transform and visualize data. These commands are always preceded by a pipe `|` character.

* **`stats`**: Calculates statistics. `| stats count by sourcetype` will count events for each sourcetype.
* **`timechart`**: Creates time-based charts. The x-axis will always represent time.
* **`chart`**: Creates charts with two different fields on the x and y axes, like `| chart count over host by log_level`.
* **`table`**: Displays results in a clean, tabular format with only the fields you specify.
* **`top` / `rare`**: Show the most or least common values for a field.
* **`sort`**: Sorts your results. Use a minus sign (`-`) for descending order.
* **`rename`**: Renames a field in your results for better readability.

***

#### Data Forwarding and Management

The session also reiterated the practical steps for getting data into Splunk from a forwarder by configuring the `inputs.conf` and `outputs.conf` files. Finally, it touched on scheduling reports to be sent via email and previewed the next session on integrating Splunk with AWS.