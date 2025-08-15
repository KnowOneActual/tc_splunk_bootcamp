### : Cloud Integration with AWS

This session was a special focus on integrating Splunk with Amazon Web Services (AWS) to pull in data directly from the cloud. The primary example was how to ingest data from an **AWS S3 bucket**.

The process was broken down into two main parts: setup in AWS and configuration in Splunk.

-----

#### Part 1: AWS Setup

Before you can get data into Splunk, you need to prepare your AWS environment.

1.  **Create an S3 Bucket**: This is the storage location in AWS where you will place the files you want Splunk to monitor and ingest.
2.  **Generate Security Credentials**: You need to create an **Access Key** and a **Secret Access Key** in the AWS IAM (Identity and Access Management) service. These keys allow Splunk to securely authenticate with your AWS account and access the S3 bucket.

-----

#### Part 2: Splunk Configuration

Once AWS is ready, you configure Splunk to connect to it.

1.  **Create a New Index**: It's a best practice to create a dedicated index in Splunk to store the incoming AWS data. This keeps it separate and easier to manage.
2.  **Install the Splunk Add-on for AWS**: From the Splunk Web UI, you navigate to **Apps \> Find More Apps** and install the official "Splunk Add-on for AWS."
3.  **Configure the Add-on**:
      * Open the newly installed AWS Add-on.
      * On the **Configuration** tab, add your AWS account using the Access Key and Secret Access Key you generated earlier.
      * Go to the **Inputs** tab and create a new input. Select **Custom Data Type \> Generic S3**.
      * Fill in the details for your S3 bucket and the new index you created.
4.  **Upload Data**: Place a file (like a CSV) into your S3 bucket. The Splunk Add-on will detect the new file and pull its contents into the index you specified.

-----

#### Part 3: Verifying the Data

To confirm that the integration is working, you simply go to the **Search & Reporting** app in Splunk and run a search on the new index:

```spl
index=<your_aws_index_name>
```

If the setup was successful, you will see the data from the file you uploaded to your S3 bucket appear in the search results.