# Dell Latitude 2120 Docker Swarm Cluster

## Objective

![Dell Latitude 2120 Cart](./images/dell_2120_cart.jpg)
![Dell Latitude 2120 Cart](./images/Dell_Latitude_2120.jpg)

The goal of this project is to use an old Dell Latitude 2120 school cart that houses 24 Dell Latitude 2120 Netbooks, from the 2010's, and create a [Docker Swarm Cluster](https://docs.docker.com/engine/swarm/) with them.

## Hardware

Here is the spec sheet on the [Dell Latitude 2120 Netbooks](./images/latitude-2120-specsheet.pdf) and the optional cart. Each of the machines has the following harware configuration:
- 1 x 2 GB 1DIMM DDR3 SDRAM (667MHz)
- 1 x 5400rpm SATA 250 GB HD

## Machine Setup

Each machine has the exact same identical initial setup:
- Debian 13 - Trixie, server no GUI and slim nothing extra loaded
- additional software installed:
  - openssh-server (apt install openssh-server)
  - [docker](https://docs.docker.com/engine/install/debian/)

The following setting have been changed, as root, on each machine:
- nano /etc/systemd/logind.conf
  - [Login]
    HandleLidSwitch=ignore
    HandleLidSwitchExternalPower=ignore
    HandleLidSwitchDocked=ignore
- nano /etc/resolv.conf
  - nameserver 10.100.204.1
- nano /etc/network/interfaces
  - # The primary network interface
    allow-hotplug enp9s0
    iface enp9s0 inet static
    address 10.100.204.150
    netmask 255.255.255.0
    gateway 10.100.204.1
    dns-nameservers 10.100.204.1
