

### Part 1: Setting Up Your AWS EC2 Instance 🖥️

First, you'll need an AWS account and a new virtual server (called an EC2 instance).

1.  **Create an AWS Account**: If you don't have one, go to the [AWS homepage](https://aws.amazon.com/) and sign up. You'll need a credit card and a phone number for verification.

2.  **Launch an EC2 Instance**:

      * From the main AWS console, search for and navigate to the **EC2** service dashboard.
      * Click the **Launch instance** button.
      * **Name**: Give your server a recognizable name, like `Splunk-Bootcamp-Server`.
      * **Application and OS Images (AMI)**: Choose **Ubuntu**. The latest "Ubuntu Server" LTS version is a great choice.
      * **Instance type**: The minimum requirement is 2 CPUs and 4 GB of RAM. The **t3.medium** instance type (2 vCPU, 4 GiB RAM) is a perfect fit. Note that this instance type is **not** covered by the AWS Free Tier.
      * **Key pair (login)**: This is crucial for accessing your server. Click **Create new key pair**, give it a name (e.g., `splunk-key`), and download the `.pem` file. **Keep this file safe; you can't download it again.**
      * **Network settings**: Click **Edit**. You need to create a security group to allow traffic on specific ports.
          * Keep the existing rule for **SSH (port 22)**. For better security, change the "Source type" to **My IP**.
          * Click **Add security group rule** and create a new **Custom TCP** rule for port **8000** (for the Splunk Web UI). Set the "Source" to **Anywhere** (0.0.0.0/0).
          * Click **Add security group rule** again and create another **Custom TCP** rule for port **9997** (for Splunk forwarding). Set the "Source" to **Anywhere**.
      * Click **Launch instance**.

-----

### Part 2: Installing and Configuring Splunk ⚙️

Now you'll connect to your server and install Splunk using the commands from your class.

1.  **Connect to Your Instance**:

      * Go back to your EC2 dashboard, select your instance, and copy its **Public IPv4 address**.
      * Open a terminal (or PowerShell on Windows) and use the key pair you downloaded to connect via SSH. The default username for Ubuntu AMIs is `ubuntu`.

    <!-- end list -->

    ```bash
    # Make sure you are in the same directory as your .pem file
    ssh -i "splunk-key.pem" ubuntu@YOUR_INSTANCE_IP
    ```

2.  **Download and Install Splunk**:

      * **Create a Splunk Account**: In your local web browser, go to [Splunk.com](https://www.splunk.com/) and create a free account.
      * **Get the Download Link**: Log into your Splunk account and navigate to the [Splunk Enterprise Downloads page](https://www.splunk.com/en_us/download/splunk-enterprise.html). Select the **.deb** package for Linux.
      * **Copy the Link**: When you click the download button, instead of saving the file, **right-click the download link and select "Copy Link Address."**
      * **Download and Install on Your Server**: Now, back in your SSH terminal, use the `wget` command with the link you just copied.

    <!-- end list -->

    ```bash
    # Download the Splunk package using the link you copied
    wget -O splunk.deb "PASTE_YOUR_DOWNLOAD_LINK_HERE"

    # Install the package
    sudo dpkg -i splunk.deb
    ```

3.  **Start and Configure Splunk**:

      * Navigate to the Splunk `bin` directory.

    <!-- end list -->

    ```bash
    cd /opt/splunk/bin/
    ```

      * Run the configuration commands you provided. These will start Splunk, accept the license, and enable it to run on boot.

    <!-- end list -->

    ```bash
    # Start Splunk and accept the license
    sudo ./splunk start --accept-license --answer-yes

    # Enable Splunk to start automatically when the server boots
    sudo ./splunk enable boot-start -user splunk

    # Set a default hostname for this Splunk instance
    sudo ./splunk set default-hostname Splunk-Bootcamp-Server
    ```

-----

### Part 3: Your First Splunk Login 🎉

Your Splunk instance is now running and ready for you to log in.

1.  **Access the Web UI**: Open a web browser and go to `http://YOUR_INSTANCE_IP:8000`. (Replace `YOUR_INSTANCE_IP` with the public IP address from your EC2 instance).

2.  **Log In**: Use the credentials that you created in Splunk setup for the first login.

   
You'll be prompted to create a new, stronger password immediately. Once that's done, you're officially in\!