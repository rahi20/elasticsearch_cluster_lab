# Creatng an Elasticsearch Cluster

The goal of this lab is to create an elasticsearch cluster of 3 nodes locally on 3 ubuntu server VMs.

![cluster archi](images/archi.png)

## Preparing the environment

We create the first VM and install Elasticsearch and Logstash on it using the following commands: 

```
sudo wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
sudo apt-get install apt-transport-https
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
sudo apt-get update && sudo apt-get install elasticsearch && sudo apt-get install logstash
```

Modify the `/etc/hosts` file to define the hostnames of the nodes in your cluster : 
```
10.5.9.22 master-00
10.5.8.168 data-00
10.5.10.204 data-01
```


Now, clone 2 other VMs. Make sure to generate new MAC@s and IP@s. (If everything is working good make sure to create snapshots)


In each VM change the hostname using : `sudo hostnamectl set-hostname <new-hostname>` and `reboot`
 
Configure static IP@s for the VMs using netplan. Cd to `/etc/netplan` and configure the conf file. 

```
network:
  version : 2
  renderer : networkd
  ethernets :
    ens33 : 
      dhcp4 : false
      addresses : [10.5.9.22/16]
      gateway4 : 10.5.0.2
      nameservers : 
        addresses :[8.8.8.8, 8.8.4.4] #Use ( nmcli dev list || nmcli dev show ) 2>/dev/null | grep DNS, to get your dns@s if public DNS is not an option.
```

## Configuring Elasticsearch


