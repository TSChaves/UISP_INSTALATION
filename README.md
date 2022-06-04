
# User tip
**Read carefully and follow the steps correctly to install the tool, I recommend using Debian 11 for installation.**



# UISP

This article describes how to install a fresh copy of UISP or update an existing installation on a console (self-hosted server/cloud platform).

## Prerequisites
#### ATTENTION: It is recommended to install UISP on a console (server) that is equipped with a public IP address and FQDN, which is directly connected to the main gateway of the network. In this setup, UISP will automatically use a valid trusted certificate through [Let's Encrypt](https://letsencrypt.org/), will report outages in the most precise manner, and all of its advanced functions will perform optimally.
#### It is certainly possible to place the UISP console (server) in a different spot in a topology, but there may be some limitations involved.

Supported Distros (LXC virtualization is not officially supported. Please use KVM):
1. [Ubuntu 16.04 LTS (Xenial Xerus)](http://releases.ubuntu.com/16.04/) 64-bit
2. [Ubuntu 18.04 LTS (Bionic Beaver)](http://releases.ubuntu.com/18.04/) 64-bit
3. [Ubuntu 20.04 LTS (Focal Fossa)](http://releases.ubuntu.com/20.04/) 64-bit
4. [Debian 11](https://www.debian.org/releases/bullseye/) 64-bit

* 2 GB RAM (Minimal)
* 16 GB of **fast SSD** storage (Minimal)
* 64-bit (x64) CPU with SSE 4.2
* Locally used ports (see [Changing the HTTP and HTTPS Ports](https://help.ui.com/hc/en-us/articles/360000119728#3) for custom ports) 
* 80 (Let's Encrypt certificate automation)
* 81 (Suspension page)
* 443 (UI, API, Devices connector)
* Allow ping (see [Devices Latency and Outage Statistics](https://help.ui.com/hc/en-us/articles/360004575834))
* A kernel with overlay2 storage driver (see [Docker Storage Drivers](https://docs.docker.com/storage/storagedriver/overlayfs-driver/))
* bash, curl, sudo (see [Installing Prerequisites](https://help.ui.com/hc/en-us/articles/360000119728#1))

## Installation Instructions

Run the command below on the host to install and start UISP (it will automatically install Docker if it is not installed already). If a UISP installation already exists, it will be overwritten, but all data will be kept. It is possible to use the --update attribute if the new installation needs to have the same parameters as the old one. 

The command below will always install the newest, **stable** version that is listed in the [Software Releases](https://community.ui.com/releases) section on the Ubiquiti Community. To view, select the **Stable** status, followed by the **UISP** tag in the **General** section.

```bash
curl -fsSL https://uisp.ui.com/v1/install > /tmp/uisp_inst.sh && sudo bash /tmp/uisp_inst.sh
```
During the installation process, the script will check if **TCP port 80** and **TCP port 443** are open/available. If the ports are in use, the script will pause and ask which ports should be used by UISP. The same applies to the overcommit memory settings. If the vm.overcommit_memory is not set to '**1**', the installation script asks for permission to enable it. In case those interrupts are unwanted in the installation process it is possible to suppress them with --unattended attribute which lets the installation script do all the necessary arrangements by itself.

When the process is complete, UISP will be accessible at the **https://ip or hostname** address. Please do not use localhost to connect to UISP.

**NOTE:** The installation script needs to use **sudo** permissions to install Docker in case it is not available in the OS already. The permissions are also needed to create the UISP user, under which the UISP application runs as well as to set up a cron task that manages the UISP updates.


# This tutorial was taken from: [UBIQUITI](https://help.ui.com/hc/en-us/articles/115012196527-UISP-Installation-Guide)
