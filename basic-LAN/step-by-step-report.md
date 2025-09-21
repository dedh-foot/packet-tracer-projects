## Table of Contents

1. [Project Overview](#project-overview)
2. [Network Topology](#network-topology)
3. [IP Addressing and Ethernet Ports](#ip-addressing-and-ethernet-ports)
4. [Device Configurations](#device-configurations)
   > 4.1 [Switch0 Configuration](#switch-configuration)

   > 4.2 [Configuring Laptop0](#configuring-laptop0)

   > 4.3 [Configuring Laptop1](#configuring-laptop1)
5. [Testing Connectivity](#testing-connectivity)
6. [Summary](#summary)


### Project Overview
This project documents the process of building a home network. It involves documentation of the design, configuration and testing of a simulated network using Cisco Packet Tracer. Included are network diagrams, device configurations and reports for reference. All screenshots, config files and diagrams are linked wherever necessary. You can also view these folders independently if you wish to.

### Network Topology
This network consists of a basic loal area network (LAN) setup with 2 laptops connected to a single switch. The switch acts as a central device that facilitates communication between the two end devices. 

 ##### Devices
 - One unmanaged switch (Switch0)
 - Two Laptops (Laptop0 & Laptop1)

 ##### Connections
  - Each laptop is connected to the switch using Ethernet Cables ("Copper Straight-Through" under the "Connections" section) 
  - The switch provides a common network segment allowing the laptops to communicate directly.

##### Network Topology Screenshot

<img width="902" height="293" alt="image" src="https://github.com/user-attachments/assets/c2f8d6f8-7846-4a6b-8728-201e4f4207ca" />

The above screenshot also show which port these connections have to be made keeping the respective devices in mind.

### IP Addressing and Ethernet Ports

This section focuses on the physical onnections between the end device and the networking devices, i.e., connections between Laptop0/Laptop1 and Switch0. The ethernet cable used is the "Copper Straight-Through" found under "Connections". Once chosen, we select the end device, which is Laptop0 and choose the "FastEthernet0" from the pop-up box. We move to Switch0 and connect to the GigabitEthernet1/0/1 from the pop-up box. This established a connetion between the two devices. For the connection to be usable, we have to wait a few seconds until the connections turn green.

We repeat the same process with Laptop1 and Switch0. We choose "FastEthernet0" on Laptop1 and "GigabitEthernet1/0/2" on Switch0 to establish a connection. This results in a basic visual simulation of a home LAN (Local Area Network).

### Device Configurations

##### Switch Configuration
The switch used for this project is the 3650-24PS Multilayer switch, i.e. Switch0.
To configure Switch0, open the device configuration window & switch it on by dragging an AC-POWER-SUPPLY on to physical device view section.
This is the device configuration window without the AC-POWER-SUPPLY:

<img width="463" height="400" alt="image" src="https://github.com/user-attachments/assets/73e7101f-4100-460e-9559-a03756ff7b49" />

This is the device configuration window after the AC-POWER-SUPPLY is attached:

<img width="464" height="400" alt="image" src="https://github.com/user-attachments/assets/bffa3c36-c750-486b-b7f1-ad37d6954df6" />

> Notice that a blank spot is filled when attaching the power supply.

Typically, a laptop is dynamically allocated an IP address using DHCP (Dynamic Host Configuration Protocol). However for this project, a different route must be taken. Since, a DHCP server is not set up for this project, we will have to manually set up the IP address for both end devices (Laptop0 & Laptop1)

##### Configuring Laptop0

In order to configure Laptop0, we open the device configuration window, select FastEthernet0, select the "Static" under "IP Configuration" and type this IP address (192.168.1.1) into the the "IPv4 Address" box. Notice that the subnet mask field is update to 255.255.255.0 after the IPv4 address is entered. Update the MAC address to this hexadecimal value 0001.1111.1111 . I changed the MAC address so that it is easy to remember. It is not possible to change the MAC address of a physical device as it is set by the manufactures during the making of the device. 

We need to configure one last thing; the default gateway. The default gateway is the "exit door" of your network. Within the same network (LAN), devices can communicate with each other utilising a typically switch. However, if any of these end devices want to access material on the internet, it will need to use this "exit door" aka default gateway. Typically, a device that conatins this defualt gateway is a router. Although, it is not essential to configure the default gateway, it has been set for educational purposes.

The default gateway is set to 192.168.1.255 and the DNS server (Domain Name System) is set to 8.8.8.8; which is the IPv4 address for Google's Public DNS servers.

The device configuration window should look like this once done. 

<img width="522" height="500" alt="image" src="https://github.com/user-attachments/assets/de1d2620-5cb4-4969-bbb4-adea1a4bc7c1" />

<img width="520" height="482" alt="image" src="https://github.com/user-attachments/assets/9cad77fa-43a9-4d8d-a94d-b7064a30b653" />


To confirm that the device has been correctly configured, we open the CLI of the device and run the "ipconfig" command into the interface. The same can be done on the end device Laptop0. Selecting the "Command Prompt" under the Desktop tab of the configuration window and run the "ipconfig" command. The output will reflect the Laptop0's network configurations. For a more detailed output, we run "ipconfig /all".

Here is the output of Laptop0 from my Packet Tracer:

https://github.com/dedh-foot/cisco-home-network/blob/bfae12067bf2b356287f5779c828c521782a1d26/screenshots/README.md

##### Configuring Laptop1

The method of configuring Laptop1 is the same as Laptop0. The method remains the same, however, the values change. The IP address for Laptop1 is configured as 192.168.1.2 which authomatically updates the subnet mask to 255.255.255.0 . Once more, I have edited the MAC address purely for my convenience to 0002.1111.1111 . the default gateway address remains the same as before, i.e. 192.168.1.255 and so does the DNS server (8.8.8.8). For further clarifications, please refer [Configuring Laptop0](#configuring-laptop0) . The configuration of Laptop1 should look like this:

<img width="550" height="300" alt="image" src="https://github.com/user-attachments/assets/bed3f868-1dba-48ba-bcbe-b51b7da82ae5" />

<img width="550" height="300" alt="image" src="https://github.com/user-attachments/assets/fbf30cc3-0375-4509-ab23-4245d3b31674" />

Here is the output of Laptop1 from my Packet Tracer:

https://github.com/dedh-foot/cisco-home-network/blob/bfae12067bf2b356287f5779c828c521782a1d26/screenshots/README.md

### Testing Connectivity

To test connectivity, it is common practice to use the command "ping". Ping is a network utility used to check if a device is reachable. It works by sending ICMP (Internet Control Message Protocol) echo packets to the target device and waiting for a reply. It tracks if the target is reachable or not, how long it takes for the target to respond (delay measured in milliseconds) and whether there was any packet loss.

Simply appending the IP address of the target device after the command (ping) does the job. So, to check connectivity between the two end devices; Laptop0 & Laptop1, we open the command prompt on each device and ping the other consecutively. 

Laptop0 to Laptop1: 
ping 192.168.1.2

Laptop1 to Laptop0:
ping 192.168.1.1

Here are the outputs to my ping requests on each device:

https://github.com/dedh-foot/cisco-home-network/blob/bfae12067bf2b356287f5779c828c521782a1d26/screenshots/README.md

### Summary 

In this short project, we created a basic home LAN (Local Area Network) using ethernet cables in Packet Tracer. The project involved connecting 2 laptops to a switch using wired conections, statically assigning IP addresses and configuring a default gateway. Through the use of simple networking commands such as ping, networking connectivity was verified. This project reinforced understanding physical cabling, IP configuration and troubleshooting within a simulated environment. This foundational exercise is a step towards creating complex network designs and configuration in the future.  

### Author
> dedhfoot  |  Cybersecurity & Networking Enthusiast 
