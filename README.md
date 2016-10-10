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

