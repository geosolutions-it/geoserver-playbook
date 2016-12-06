# geoserver-playbook
An ansible playbook to deploy geoserver on a cluster

It installs on each cluster node java, tomcat and geoserver with extensions on a RedHat7/CentOS7.

# How to use this playbook
You first have to setup an **Ansible control machine**, a desktop or server linux machine where python and ansible are installed.

Once the Ansible control machine is set this playbook can be used to provision cuncurrently N target machines reachable from the control machine.

## Setting up the control machine

* Create a fresh Linux virtual machine, any other disto should be fine. (Following instructions for Ubuntu 12/14)
* Install python and pip of they aren't installed yet

  `#root$ sudo apt-get install python python-pip`
  
* Install some other python packages required to ansible

  `#root$ sudo pip install paramiko PyYAML Jinja2 httplib2 six`
  
* Then install ansible from sources. apt and yum repositories has recent versions of ansible but very often some [Extras modules](http://docs.ansible.com/ansible/modules_extra.html) are not included
  ```
   #root$ git clone git://github.com/ansible/ansible.git --recursive   # Don't forget --recursive !!!
   #root$ cd ./ansible
   #root$ source ./hacking/env-setup  #set env variables valid only in the current shell
  ```
  This playbook is tested with ansible 2.3 (master branch atm)
 
 * Check if everything works running the ping module
   `#root$ ansible all -m ping -u root --ask-pass`
   
Check for more info on the [ansible official documentation](http://docs.ansible.com/ansible/intro_installation.html#running-from-source)

## Run the playbook

* Clone this repo
  `#root$ git clone git@github.com:geosolutions-it/geoserver-playbook.git`

* Run the playbook with
  `#root$ sudo ansible-playbook -v -i hosts playbook.yml -u root -k`
  
  * **-v** Set the verbosity of the log (add more v)
  * **-u** The user used by ansible to connect to target VMs
  * **-k** use password authentication, by default it uses ssh-key

### Playbook configuration

* Set in the `hosts` file the IPs/domain names of the target machines
* Configure in `playbook.yml` all the parameters, add more instances under the `tomcat_instances` block to deploy more java containers
* The geoserver extensions configuration is in `roles/geosolutions.geoserver/vars/main.yml`. An issue is open to better externalize this config
  
  
  
  
