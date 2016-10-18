# vtechworks: Ansible

Deployment Tool for VTechworks

[![LICENSE](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](./LICENSE)

## Introduction

These files can be used to install the Vtechworks either to a VM under VirtualBox. Installation is done via Vagrant. Alternatively, Ansible may be used directly to set up the application on a suitable target system.

## Installation

These scripts are intended to be run on a Unix-like system. They are tested to work on Mac OSX and Ubuntu Trusty Tahr.

To use these scripts [Vagrant](https://vagrantup.com) must already have been installed on the local system with the [Virtual](https://virtualbox.org) provider working.

You will need version 1.6+ of [Vagrant](https://vagrantup.com) installed on the local system.

In addition [Ansible](https://ansible.com) at least 2.1+ will need to be installed. On Mac OS this can be installed via [Homebrew](https://brew.sh)
using the following command

```
brew install ansible
```

*On Ubuntu Trusty*

```
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible
```

Clone this repository on your local machine using git which is installed using the following command
```
brew install git
```

*On Ubuntu Trusty*

```
sudo apt-get install git
```

## Configuration

A deployment settings file needs to be created in the `ansible` directory. This file is called `site_secrets.yml` and can be created by copying the example file `example_site_secrets.yml` with the following command from the cloned repository:

```
cp ansible/example_secrets.yml ansible/site_secrets.yml`
```

The Ansible playbook will be expecting a repository-ignored `site_secrets.yml` YAML file. Read the variable contents of the file and adjust them to match your local environment.

## Usage

In the case of a local development environment the user will need to install maven software and its java dependencies on the host. Once again using [Homebrew](https://brew.sh) install maven.

```
brew install Caskroom/cask/java
brew install maven32
```

*On Ubuntu Trusty*

```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
sudo apt-get purge -y maven
# download maven 3.2.5 from https://maven.apache.org/download.cgi to temp dir
sudo tar -zxf /tmp/apache-maven-3.2.5-bin.tar.gz -C /opt/nondeb/
sudo ln -s /opt/nondeb/apache-maven-3.2.5/bin/mvn /usr/local/bin/mvn
echo "export M2_HOME=/opt/nondeb/apache-maven-3.2.5" >> ~/.profile
. ~/.profile
```


Note that the `Vagrantfile` expects VTUL's fork of [DSpace](https://github.com/vtul/vtechworks.git) to be on your host machine at `dspace` of your cloned repo where you will do your development.

In `dspace/config/dspace.cfg`, change

```
event.dispatcher.default.consumers = versioning, discovery, eperson, harvester, elements
```
to

```
event.dispatcher.default.consumers = versioning, discovery, eperson, harvester
```

Then, from the cloned  `vtechworks-ansible` directory, build the DSpace project using Maven.

```
cp ansible/roles/vtechworks/templates/build.properties.j2 dspace/dspace_local.properties
cd dspace
git checkout vt_5_x_dev
mvn clean package -Denv=dspace_local -Dmirage2.on=true
```

To install a pristine (recommend this after every sprint test) VTechworks installation using the new configurations, do the following from the directory you just cloned:

```
vagrant box update
vagrant up
```

## VA Tech ONLY steps to complete local development installation

We will be deleting the default Dspace database to install a sample of records for your development. Download the database from Google Drive/VTechWorks/Technology/fewer_items_database_dump.sql.gz to `vtechworks-ansible` and uncompress the file then run the following steps:

```
vagrant ssh
sudo /usr/sbin/service tomcat7 stop
sudo netstat -tlnp
```

Kill the process that owns the 8080 pid if it fails to stop tomcat7. If the process is 12345 we will kill it with:

```
sudo kill -9 12345
```

We can then import the database above with the following steps.

```
cd /dspace/bin
sudo -s
./dspace database clean
sudo -u postgres psql dspace < /vagrant/fewer_items_database_dump.sql
./dspace database migrate
sudo -u vtechworks /dspace/bin/dspace index-discovery -b
sudo /usr/sbin/service tomcat7 restart
```

## For Ansible Deployment

If you are using Ansible directly, you will need the IP address of the server you plan to provision. You can the run the following command from the directory you just cloned:

```
ansible-playbook --limit <ip address> site.yml -b
```

### Local VM

In the case of the `vagrant up` option, a VM will be brought up and configured in the current directory. The application is accessible on the local machine from a Web browser at the URI http://192.168.60.4 .

You can use vagrant ssh to log in to this VM when it is up. When logged out of the VM, vagrant halt can be used to shut down the VM. The command vagrant destroy will destroy it entirely, requiring another vagrant up to recreate it.

### Ansible

When using Ansible to provision directly, the playbook will be executed on the server whose IP address is given as IP. When the playbook finishes with no failures, the server is accessible at this URL:

```
http://<ip address>
```

or

```
https://<ip address>
```
