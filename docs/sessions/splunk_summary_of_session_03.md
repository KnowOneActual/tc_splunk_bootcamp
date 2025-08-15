
### Summary of Session 3: Search Processing Language (SPL) & Deployment

This session covered the fundamentals of Splunk's Search Processing Language (SPL), basic deployment architectures, and a practical guide to forwarding data.

#### What is Search Processing Language (SPL)?

**SPL** is the query language used to search, analyze, and visualize data within Splunk. It allows you to interact with your data to filter it, find specific information, and extract meaningful insights.

A basic search starts by specifying an **index** and can be refined with keywords and a **time range**.

**Key SPL Commands:**

* `stats`: Used to aggregate data and calculate statistics like `count`, `sum`, and `avg`.
* `top`: Shows the most frequent values for a specific field.
* `timechart`: Creates time-series charts to visualize data over time.
* `sort`: Sorts your results. Use a minus sign (`-`) to sort in descending order.
* `rename`: Renames a field in your search results for clarity.

#### Splunk Deployment Architectures

Splunk can be deployed in several ways depending on the scale and needs of the environment:

1.  **Standalone Deployment**: A single Splunk instance handles everything: data input, parsing, indexing, and searching. This is great for learning or small-scale use, but lacks high availability.

2.  **Distributed Deployment**: The roles are split across different components:
    * **Forwarders**: Lightweight agents that collect and send data.
    * **Indexers**: Receive, parse, and store the data.
    * **Search Head**: Provides the user interface for searching the data stored on the indexers.

3.  **Clustered Deployment**: This is the standard for production environments. It builds on the distributed model by adding redundancy and high availability.
    * **Indexer Cluster**: A group of indexers that replicate data (usually three copies) to prevent data loss if one indexer goes down.
    * **Search Head Cluster**: A group of search heads, often behind a load balancer, to handle many concurrent users without performance issues.

#### Dashboards

Dashboards are collections of panels that visualize your data. Panels can contain charts, tables, maps, and search boxes. You can create a new dashboard by saving a search query as a panel or add new panels to an existing dashboard.

#### Practical: Configuring a Universal Forwarder

The session included a hands-on example of forwarding logs from a separate server to a Splunk instance:

1.  **On the Forwarder (your source server)**:
    * Install the Splunk Universal Forwarder package.
    * Configure `outputs.conf` to point to your main Splunk instance's IP address and port `9997`.
    * Configure `inputs.conf` to `monitor` a specific file or directory (e.g., `/var/log/syslog`).

2.  **On the Splunk Indexer (your main instance)**:
    * Go to **Settings > Forwarding and receiving**.
    * Configure Splunk to **receive data** on port `9997`.

After restarting the forwarder, data from the monitored file will begin appearing in your main Splunk instance.