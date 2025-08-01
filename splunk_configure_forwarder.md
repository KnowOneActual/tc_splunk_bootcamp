
## Configuring a Splunk Universal Forwarder

These steps outline the basic configuration for a new Splunk Universal Forwarder on a Linux system. You'll create local versions of `outputs.conf` and `inputs.conf` to override the default settings.

-----

### Step 1: Configure `outputs.conf`

This file tells the forwarder where to send its data, which is typically one or more Splunk indexers.

First, create and edit the file in the local configuration directory:

```bash
sudo nano /opt/splunkforwarder/etc/system/local/outputs.conf
```

Next, add your indexer information. This configuration directs all data to a single destination. Remember to replace `10.0.1.100:9997` with your indexer's actual IP address and receiving port.

```ini
[tcpout]
defaultGroup = default-autolb-group

[tcpout:default-autolb-group]
server = 10.0.1.100:9997
```

-----

### Step 2: Configure `inputs.conf`

This file specifies which local files and logs the forwarder should monitor.

Create and edit the inputs file:

```bash
sudo nano /opt/splunkforwarder/etc/system/local/inputs.conf
```

Add a stanza for each data source you want to collect. The examples below monitor the primary system and authentication logs on a typical Ubuntu server.

```ini
# Monitor the main system log
[monitor:///var/log/syslog]
disabled = false
index = os
sourcetype = syslog

# Monitor authentication logs (SSH, sudo, etc.)
[monitor:///var/log/auth.log]
disabled = false
index = os
sourcetype = linux_secure
```

  * `[monitor:///path/to/file]` defines the file or directory to watch.
  * `index = os` tells Splunk where to store the data.
  * `sourcetype = linux_secure` helps Splunk correctly classify and parse the data.

-----

### Step 3: Apply Changes

A restart is required to load the new configurations.

```bash
sudo /opt/splunkforwarder/bin/splunk restart
```

After restarting, the forwarder will begin monitoring your specified files and sending the data to your indexer.