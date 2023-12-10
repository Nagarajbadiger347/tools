# Install Prometheus
Create a system user or system account

    sudo useradd \
    --system \
    --no-create-home \
    --shell /bin/false prometheus
Use the curl or wget command to download Prometheus

    wget https://github.com/prometheus/prometheus/releases/download/v2.47.1/prometheus-2.47.1.linux-amd64.tar.gz
Extract all Prometheus files from the archive

    tar -xvf prometheus-2.47.1.linux-amd64.tar.gz
Create a /data directory. Also, you need a folder for Prometheus configuration files.

    sudo mkdir -p /data /etc/prometheus
Change the directory to Prometheus and move some files

    cd prometheus-2.47.1.linux-amd64/
    sudo mv prometheus promtool /usr/local/bin/
    sudo mv consoles/ console_libraries/ /etc/prometheus/
    sudo mv prometheus.yml /etc/prometheus/prometheus.yml
To avoid permission issues, you need to set the correct ownership for the /etc/prometheus/ and data directory.

    sudo chown -R prometheus:prometheus /etc/prometheus/ /data/
Delete the archive and a Prometheus folder when you are done

    cd
    rm -rf prometheus-2.47.1.linux-amd64.tar.gz
Verify that you can execute the Prometheus binary by running the following command:

    prometheus --version

Use some of these options in the service definition.
We're going to use Systemd, which is a system and service manager for Linux operating systems. For that, we need to create a Systemd unit configuration file.

        sudo vim /etc/systemd/system/prometheus.service
Prometheus.service
        
        [Unit]
        Description=Prometheus
        Wants=network-online.target
        After=network-online.target
        
        StartLimitIntervalSec=500
        StartLimitBurst=5
        
        [Service]
        User=prometheus
        Group=prometheus
        Type=simple
        Restart=on-failure
        RestartSec=5s
        ExecStart=/usr/local/bin/prometheus \
          --config.file=/etc/prometheus/prometheus.yml \
          --storage.tsdb.path=/data \
          --web.console.templates=/etc/prometheus/consoles \
          --web.console.libraries=/etc/prometheus/console_libraries \
          --web.listen-address=0.0.0.0:9090 \
          --web.enable-lifecycle
        
        [Install]
        WantedBy=multi-user.target
Important options related to Systemd and Prometheus. Restart - Configures whether the service shall be restarted when the service process exits, is killed, or a timeout is reached.
RestartSec - Configures the time to sleep before restarting a service.
User and Group - Are Linux user and a group to start a Prometheus process.
Config.file=/etc/prometheus/prometheus.yml - Path to the main Prometheus configuration file.
Storage.tsdb.path=/data - Location to store Prometheus data.
Web.listen-address=0.0.0.0:9090 - Configure to listen on all network interfaces. In some situations, you may have a proxy such as nginx to redirect requests to Prometheus. In that case, you would configure Prometheus to listen only on localhost.
Web.enable-lifecycle -- Allows to manage Prometheus, for example, to reload configuration without restarting the service.

To automatically start the Prometheus after reboot, run enable.

        sudo systemctl enable prometheus
start the Prometheus.

        sudo systemctl start prometheus
To check the status of Prometheus run the following command:

        sudo systemctl status prometheus
Issues with Prometheus or are unable to start it. The easiest way to find the problem is to use the journalctl command and search for errors.

        journalctl -u prometheus -f --no-pager
