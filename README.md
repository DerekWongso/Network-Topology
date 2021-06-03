# Network Topology Setup

This project will demonstrate how to setup a basic network topology with the assistance of **Cisco Packet Tracer.** 
**Cisco Packet Tracer** is a simulation tool built by Cisco to help educate and train individuals on how to build networks across a multitude of devices.

### Step 1
Set up the router and two switches. Then connect them with the Copper-Straight-Through wire connection.

![github-small](https://github.com/DerekWongso/Network-Topology/blob/3dfb1fe3b4ef15e55ee5005c8b51e3f2a382cb32/Images/r%26s.png)

### Step 2
Go to your router settings, click the **Command Line Interface** or **CLI** and input these commands to give your router a host name. In the image below, I named my router **DWR1**

**en/**
**conf t/**
**hostname routername**

![github-small](https://github.com/DerekWongso/Network-Topology/blob/3dfb1fe3b4ef15e55ee5005c8b51e3f2a382cb32/Images/dwr1.png)


The same steps apply for the two switches as well. It is best to also give them host names to keep it orderly. In this project, I named my switches **DWSW1** and **DWSW2**

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

### Step 6
On this step, we will give the router a static default route IP. As a sample, I made my static default route IP 204.186.29.3

**en/**
**conf t/**
**ip route 0.0.0.0 0.0.0.0 ip address**

![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/r1ipadd.png)

### Step 7
We can also integrate **DHCP** into our network. **DHCP** or **Dynamic Host Configuration Protocol** is a protocol used to automate and manage multiple devices on IP networks, allowing the use of services such as DNS or NTP. To set it up, you go to the **CLI** on your router and input:

**ip dhcp pool name/**
**network ip and subnet/**
**dns-server ip address/**
**exit/**
**dhcp excluded-address ip scope**

For example, I named the DHCP **DWNet,** made the DNS server 192.168.20.18, and excluded a particular scope of addresses including address 254.

![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/dhcpdns.png)

### Step 8
You can construct an access list on the router to deny IP traffic from certain addresses. You can input this into the router's **CLI:**

**access-list 1 deny ip address and subnet mask/**
**access-list permit any/**
**int g0/1/**
**ip access-group 1 in**

As a sample, I denied access to the IP and subnet of 117.23.54.0 0.0.0.255. The permit any command is also important because all other traffic will not be present if it is not used. 

![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/denypermit.png)

### Step 9
You can set up **SSH** on all your devices. **SSH** or **Secure Shell Protocol** is a protocol which it helps provide a secure channel over an unsecured network. It utilizes a client-server style of protocol. You can input these commands to create a domain name, a rsa key, and ultimately enable **SSH**

**ip domain-name name/**
**crypto key generate rsa/**
**ip ssh version 2/**
**line vty 0 4/**
**transport input ssh**
**login local**

For this case, my domain name is **DECKKINGMASTER.LOCAL.** I made the key 2048 bits as it is the most secure.

![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/ssh.png)

### Step 10
For all our devices, this step will help lock out the Aux port, disable the http engine, disable **Cisco Discovery Protocol,** and set a password for the console port. You can input this on the router and switch **CLI:**

**service password-encryption/**
**line aux 0/**
**exec-timeout 0 0/**
**exit/**
**line con 0/**
**password password/**
**exit/**
**no cdp run**

![github-small](https://github.com/DerekWongso/Network-Topology/blob/main/Images/auxcdp.png)
