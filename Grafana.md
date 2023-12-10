Check and install all the dependencies which are required

    sudo apt-get install -y apt-transport-https software-properties-common
Add the GPG keyAfter you add the repository, update and install Garafana.

    wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
Add this repository for stable releases

    echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

After you add the repository, update and install Garafana.

    sudo apt-get update
    sudo apt-get -y install grafana
To automatically start the Grafana after reboot, enable the service

    sudo systemctl enable grafana-server
Start the Grafana

    sudo systemctl start grafana-server
To check the status of Grafana

    sudo systemctl status grafana-server

