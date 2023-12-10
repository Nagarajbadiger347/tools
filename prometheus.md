# Install Prometheus
create a system user or system account

    sudo useradd \
    --system \
    --no-create-home \
    --shell /bin/false prometheus
use the curl or wget command to download Prometheus

    wget https://github.com/prometheus/prometheus/releases/download/v2.47.1/prometheus-2.47.1.linux-amd64.tar.gz
extract all Prometheus files from the archive

    tar -xvf prometheus-2.47.1.linux-amd64.tar.gz
create a /data directory. Also, you need a folder for Prometheus configuration files.

    sudo mkdir -p /data /etc/prometheus
Change the directory to Prometheus and move some files

    cd prometheus-2.47.1.linux-amd64/
    sudo mv prometheus promtool /usr/local/bin/
    sudo mv consoles/ console_libraries/ /etc/prometheus/
    sudo mv prometheus.yml /etc/prometheus/prometheus.yml
To avoid permission issues, you need to set the correct ownership for the /etc/prometheus/ and data directory.

    sudo chown -R prometheus:prometheus /etc/prometheus/ /data/
 delete the archive and a Prometheus folder when you are done

    cd
    rm -rf prometheus-2.47.1.linux-amd64.tar.gz
Verify that you can execute the Prometheus binary by running the following command:

    prometheus --version
