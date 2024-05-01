# So you want to be a SOC Analyst? by Eric Capuano

This lab was created by Eric Capuano. It can be found at <a href="https://blog.ecapuano.com/p/so-you-want-to-be-a-soc-analyst-intro">https://blog.ecapuano.com/p/so-you-want-to-be-a-soc-analyst-intro</a>. "A blog series for someone wanting to get a start as a SOC Analyst."

## Objective

The SYWTBSA project aimed to establish a controlled environment for simulating and detecting cyber attacks. This hands-on experience was designed to develop direct and indirect skills such as deploying and configuring systems, routers, firewalls, parse logs, tuning Sysmon, etc. for network security, detection and response.

### Skills Learned

- 
- 
- 

### Tools Used

- 
- 
- 

## Steps


1. The first task was to download and install a free 30-day trial version of VMware rkstation.
   This part was self explanatory. Trial should end May 30th. Countdown begins.

2. Download and deploy a free VMware version of Windows VM directly from Microsoft.
   This VM will be deployed with 4GB of RAM at the start as my laptop only has 16GB as the host system. We will allocate more when needed.

3. Download and install the Ubuntu Server 22.04.1 ISO into a new VM.
   Per Eric's instructions, 2GB of RAM and 2 cores will be allocated.

   We are instructed to set static IP for this lab. This requires getting the subnet IP and gateway IP.
   Not explicitly stated in the Lab, but note that the subnet ID is ending with /24. Thus, if needed, we know that the subnet mask will be 255.255.255.0 from our training in Net+. 11111111.11111111.11111111.0 => 24 "on" bits followed by 8 "off" bits making 32-bit subnet mask.

   The reason for static IP is so that DHCP does not lease new IPs throughout the course of this lab.

   Subnet IP: 192.168.232.0
   Subnet Mask: 255.255.255.0
   Gateway IP: 192.168.232.2

   VM IP: 192.168.232.128/24

