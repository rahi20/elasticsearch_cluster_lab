# Creatng an Elasticsearch Cluster

The goal of this lab is to create an elasticsearch cluster of 3 nodes locally on 3 ubuntu server VMs. (Make sure to generate new MAC@s and IP@s for the vms if you are cloning).

First change the hostnames, to know which is which. We use :
```sudo hostnamectl set-hostname <new-hostname>```
  
and `reboot`
 
Configure static IP@s for the VMs using netplan. Cd to /etc/netplan and configure the conf file. 

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
