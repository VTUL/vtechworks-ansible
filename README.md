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

Clone this repository on your local machine.

## Configuration

A deployment settings file needs to be created in the `ansible` directory. This file is called `site_secrets.yml` and can be created by copying the example file `example_site_secrets.yml` with the following command from the cloned repository:

```
cp ansible/example_secrets.yml ansible/site_secrets.yml`
```

The Ansible playbook will be expecting a repository-ignored `site_secrets.yml` YAML file. Read the variable contents of the file and adjust them to match your local environment.
