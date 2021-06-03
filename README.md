# Network Topology Setup

This project will demonstrate how to setup a basic network topology with the assistance of **Cisco Packet Tracer.** 
**Cisco Packet Tracer** is a simulation tool built by Cisco to help educate and train individuals on how to build networks across a multitude of devices.

### Step 1
Set up the Router and two Switches. Then connect them with the Copper-Straight-Through wire connection.

![github-small](https://github.com/DerekWongso/Network-Topology/blob/3dfb1fe3b4ef15e55ee5005c8b51e3f2a382cb32/Images/r%26s.png)

### Step 2
Go to your router settings, click the **Command Line Interface** or **CLI** and input these commands to give your router a host name. In the image below, I named my router **DWR1**

**en/**
**conf t/**
**hostname routername**

![github-small](https://github.com/DerekWongso/Network-Topology/blob/3dfb1fe3b4ef15e55ee5005c8b51e3f2a382cb32/Images/dwr1.png)


The same steps apply for the two Switches as well. It is best to also give them host names to keep it orderly. In this project, I named my Switches **DWSW1** and **DWSW2**

![github-small](https://github.com/DerekWongso/Network-Topology/blob/3dfb1fe3b4ef15e55ee5005c8b51e3f2a382cb32/Images/dwsw1.png)

You can also change their display name to match their host names through their respective settings

![github-small](https://github.com/DerekWongso/Network-Topology/blob/3dfb1fe3b4ef15e55ee5005c8b51e3f2a382cb32/Images/display1.png)
![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/display2.png)

Now if you traverse to the topology display, the display should also show the host names as well.

![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/topology.png)

### Step 3
Now we go configure all the devices to set up usernames, their passwords, and their privileges. To do that, you go to the CLI and input these commands

**en/**
**conf t/**
**user username priv 1-15 secret password**

In this demonstration, I set up 3 accounts: **Root**, **Admin**, and **Guest**. You can give them any privilege level or password.

![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/userpw.png)

### Step 4
To set up the IP adressess for the switches, you must input these commands into your router's **CLI:**

For switch 1:
**en/**
**conf t/**
**int g0/0/**
**ip add ip address and subnet mask/**
**no shut**

For switch 2:
**en/**
**conf t/**
**int g0/1/**
**ip add ip address and subnet mask/**
**no shut**

For my first switch, I gave it the IP address 192.168.20.1 and the subnet mask 255.255.255.0
For the second switch, I gave it the IP address 204.186.29.1 and the subnet mask 255.255.255.248

![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/ip.png)

### Step 5
Here, we can set up **VLAN** or **Virtual Local Area Network.** **VLAN** is a custom netowork which lets a group of devices that are available in many networks to be fused into a logical network. In this case, we will be giving the **VLAN** interface IP addresses for both switches. For this demonstration, I made the **VLAN** IP addresses and subnet for  switch 1 192.168.20.254 255.255.255.0 and for switch 2 204.186.29.2 255.255.255.248. The commands for the **CLI** are:

**en/**
**conf t/**
**vlan number/**
**name name/**
**exit/**
**int vlan number/**
**ip add ip address and subnet mask/**
**exit**

![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/sw1Vlan.png)
![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/sw2vlan.png)

To add connection to fast ethernet:

**int f0/1/**
**switchport mode access/**
**switchport access vlan number**


Lastly, to test the connectivity, you can ping the ip address of the **VLAN** and switch itself:

**exit/**
**ping ip address**

![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/sw1connect.png)
![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/sw2connect.png)

