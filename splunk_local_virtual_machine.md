##Setting up a local virtual machine is a great, cost-effective way to run a Splunk instance for learning and testing.

###Here is a complete guide to installing Splunk on an Ubuntu Server running in VirtualBox.

-----

### **Part 1: Prerequisites & Downloads**

Before you begin, you need to download two pieces of free software.

1.  **Download VirtualBox**: If you don't already have it, download and install the latest version of [Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads) for your operating system (Windows, macOS, or Linux).

2.  **Download Ubuntu Server**: You'll need the installation file for Ubuntu Server.

      * Go to the [Ubuntu Server download page](https://ubuntu.com/download/server).
      * Download the latest **LTS (Long-Term Support)** version. This will be an `.iso` file.

-----

### **Part 2: Creating the Ubuntu Virtual Machine**

Next, you'll create and configure the virtual machine (VM) that will run Ubuntu and Splunk.

1.  **Create a New VM**:

      * Open VirtualBox and click the **New** button.
      * **Name**: Give your VM a descriptive name, like `Splunk-Ubuntu-VM`.
      * **ISO Image**: Select the Ubuntu Server `.iso` file you just downloaded.
      * **Skip Unattended Installation**: Make sure to check the box for **Skip Unattended Installation**. This lets you manually configure the server, which is better for this use case.
      * Click **Next**.

2.  **Allocate Hardware**:

      * **Base Memory**: Set the slider to at least **4096 MB** (4 GB).
      * **Processors**: Set the slider to at least **2 CPUs**.
      * Click **Next**.

3.  **Create Virtual Hard Disk**:

      * Accept the default **Create a Virtual Hard Disk Now** option. A size of **25 GB** is plenty.
      * Click **Next**, and then **Finish**.

4.  **Configure Networking**:

      * With your new VM selected in VirtualBox, click the **Settings** button.
      * Go to the **Network** section.
      * On the **Adapter 1** tab, change **Attached to:** from `NAT` to **Bridged Adapter**. This will make your VM appear as a separate device on your local network, making it much easier to access the Splunk web interface from your main computer.
      * Click **OK**.

-----

### **Part 3: Installing Ubuntu Server**

Now it's time to install the Ubuntu operating system on your new VM.

1.  **Start the VM**: Select your VM and click the **Start** button.

2.  **Follow the Installer**: The Ubuntu installer will launch. Use your keyboard to navigate through the steps:

      * Select your language.
      * Choose your keyboard layout.
      * Select the default **Ubuntu Server** installation type.
      * The installer will automatically detect the network settings.
      * Do not configure a proxy.
      * Use the default mirror address for Ubuntu's archives.
      * For storage, use the default option (**Use an entire disk**).
      * Confirm the storage configuration.
      * **Profile setup**: Create your user account. Pick a username and password you'll remember.
      * **SSH Setup**: When prompted, choose **Install OpenSSH server**. This is important for managing your VM later.
      * **Featured Server Snaps**: You can skip this; don't select any of the optional server software.
      * The installation will now proceed. Once it's complete, select **Reboot Now**.

-----

### **Part 4: Installing and Configuring Splunk**

Your Ubuntu Server is running. The final step is to install and set up Splunk.

1.  **Log into Your VM**: After the reboot, you'll see a login prompt in the VirtualBox window. Log in with the username and password you created during the Ubuntu installation.

2.  **Find Your VM's IP Address**: You need the IP address to access Splunk later. Run this command:

    ```bash
    ip a
    ```

    Look for the IP address listed under the `enp0s3` or similar interface (e.g., `192.168.1.15`). Write this down.

3.  **Download and Install Splunk**:

      * **Create a Splunk Account**: On your main computer's browser, go to [Splunk.com](https://www.splunk.com/) and create a free account.
      * **Get the Download Link**: Log into your Splunk account and navigate to the [Splunk Enterprise Downloads page](https://www.splunk.com/en_us/download/splunk-enterprise.html). Select the **.deb** package for Linux.
      * **Copy the Link**: When you click the download button, instead of saving the file, **right-click the download link and select "Copy Link Address."**
      * **Download and Install on Your VM**: Now, back in your VM's terminal, use the `wget` command with the link you just copied.

    <!-- end list -->

    ```bash
    # Download the Splunk package using the link you copied
    wget -O splunk.deb "PASTE_YOUR_DOWNLOAD_LINK_HERE"

    # Install the package
    sudo dpkg -i splunk.deb
    ```

4.  **Start and Configure Splunk**:

      * Navigate to the Splunk `bin` directory.

    <!-- end list -->

    ```bash
    cd /opt/splunk/bin/
    ```

      * Run the configuration commands from your class.

    <!-- end list -->

    ```bash
    # Start Splunk and accept the license
    sudo ./splunk start --accept-license --answer-yes

    # Enable Splunk to start automatically when the server boots
    sudo ./splunk enable boot-start -user splunk

    # Set a default hostname for this Splunk instance
    sudo ./splunk set default-hostname Splunk-VM
    ```

-----

### **Part 5: Your First Splunk Login 🎉**

Your Splunk instance is now running inside your VirtualBox VM.

1.  **Access the Web UI**: On your **host computer** (your main machine, not the VM), open a web browser and go to `http://YOUR_VM_IP:8000`. (Replace `YOUR_VM_IP` with the IP address you found in step 4.2).

2.  **Log In**: Use the default credentials for the first login:

      * **Username**: `admin`
      * **Password**: `changeme`

You'll be prompted to create a new, stronger password. Once that's done, you are officially running Splunk on your local machine\!