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


### Part 1: Setting up 2 small VMs

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

4. Disable Defender on Windows VM
   I find it neat to learn that in Win11 Defender will turn itself back on, so several settings need to be turned off as well as GPO and Registry need to be edited.

5. Prevent the VM from goign on standby by changing some power configs.

6. Install Sysmon in Windows VM
   Sysmon is short for System Monitor which is a great tool for analysts to get granular telemetry on Windows endpoint. Sysmon logs system activity to the event log such as process creations, network connections, file changes, etc. Think WireShark but for your System.

7. Install LimaCharlie EDR on Windows VM
   LC is a "SecOps Cloud Platform" that comes with cross-platform EDR agent. It also handles log shipping/ingestion and has a threat detection engine. SecOps, or Security Operations, is a collaborative approach to cyber security between IT Security and IT Operations to ensure all processes can perform and operate safely and securely. EDR, or Endpoint Detection & Response is a client-side ( hence, endpoint) security solution that monitors enpoints to detect and respond to cyber threats like randsomware and malware. Log shipping refers to the process of automating the backup of transaction log files form a primary database server to a secondary standby server.
   LC will start shipping Sysmon logs.

8. At this time, we will take a snapshot of the VMs as the baseline in case we need to scrap the project and start fresh.

9. We will now setup the attack system. We'll be using SSH on the host to connect to the Ubuntu VM which will make future CLI activities easier with copy/paste "magic"
   ssh user@192.168.232.128

10. Drop into root sheel using "sudo su" command and run command given from lab to download Sliver, a Command & Control (C2) framework. C2 is the infrastructure used by and attacker that contains a collection of tools and methods used to communicate with the compromised devices.

11. MAke a future working directory according to the lab.

12. Explore LC web interface to learn more about what it can do.
   Go to "Sensors List" and click on the hostname of the sensor we installed today and explorer these options to start with.
   - Timeline
            It's odd that the time and date seems to be incorrect: today's date is 5/1/2024 but the date here is 5/2/2024.
            Ahh, it makes sense now, the time is not based off of the Windows VM but ratehr ont he Ubuntu Server VM and Ubuntu uses UTC
   - Processes
        - Real-time list of process activity
   - Network
        - Real-time list of active network conenctions and listening ports
            So, this is like your netstat if you're familiar with netstat.
   - File System
        - Browse the entire system!
            Here, we can navigate through the different Drives, in this case it start at the C-drive. We can see the file name, path, along with other detials regarding the file including inspectign the hash and downloading the file. One use is we can grab the file and port it to a sandbox for malware analysis ont he backend.
   - Autoruns
        - We can detect anomolies that is set to autorun on the system here.
   
