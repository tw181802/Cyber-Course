# Cyber-Course
SIEM

Azure
SIEM & Honeypot | Microsoft Azure Sentinel Attack Map

Summary
SIEM (Security Information and Event Management System):
SIEM helps organizations detect, analyze, and respond to security threats.
It collects event log data from various sources in a network (like Firewalls, IDS/IPS, Identity solutions).
Security professionals use SIEM to monitor, prioritize, and address potential threats in real-time.
Honeypot:
A honeypot is a security mechanism.
It creates a virtual trap in a controlled environment to lure attackers.
By intentionally compromising a computer system, security experts study attacker behavior, explore different threats, and enhance security policies.
Lab Purpose:
Understand how to collect honeypot attack log data.
Query this data using a SIEM (like Microsoft’s Azure Sentinel).
Display it in an easy-to-understand format, such as a world map showing attack counts and geolocations.
Learning Objectives:
Configure and deploy Azure resources (virtual machines, Log Analytics Workspaces, and Azure Sentinel).
Gain hands-on experience with Azure Sentinel (a SIEM tool).
Learn about Windows Security Event logs.
Use KQL (Kusto Query Language) to query logs.
Create a dashboard (using Workbooks) to display attack data on a world map.
Tools & Requirements:
Microsoft Azure Subscription.
Azure Sentinel.
Kusto Query Language (KQL) for building the world map.
Network Security Groups (Azure’s Layer 4/3 Firewall).
Remote Desktop Protocol (RDP).
Third-party API: ipgeolocation.io.
Custom PowerShell script by Josh Madakor or Your own Personal Script



Setting Up the Honeypot in Azure VM

Create your Azure free account
Login w/ Microsoft Acct and use Azure

PERKS:
Popular services free for 12 months
55+ services always free
$200 credit to use in your first 30 days (delete resource group when done it’ll eat up subscription cost )
No automatic charges
After your credit is over, we’ll ask you if you want to continue with pay-as-you-go. If you do, you’ll only pay if you use more than the free amounts of services.	



![Screenshot 2024-06-15 at 2 52 06 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/91de71c8-6e02-4504-883b-c717097eebda)







Go to your Portal and (Virtual Machines)
Go to portal.azure.com
Search for "virtual machines"

Create a virtual machine and I named mines Thoneypot-vm and create a resource group and configured it with Windows 10
Project details
Create new resource group and name it (honeypotlab)
A resource group is a collection of resources that share the same lifecycle, permissions, and policies.

Instance details
Name your VM (Thoneypot-vm)
Select a recommended region ((US) East US 2)
Availability options: No infrastructure redundancy required
Security type: Standard
Image: Windows 10 Pro, version 21H2 - x62 Gen2
VM Architecture: x64
Size: Default is okay (Standard_D2s_v3 – 2vcpus, 8 GiB memory)


Setting Up the Honeypot in Azure VM
1. Create a Azure Account and Deploy Virtual Machine (VM):
o Set up a VM that will act as the honeypot and expose it to the internet.
o Configure the instance details, including networking settings.
o Deploy the VM, ensuring it’s accessible from the internet.



![Screenshot 2024-06-09 at 7 34 43 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/465077cc-e899-415e-b1b0-d67bab093032)



![Screenshot 2024-06-09 at 7 36 26 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/f52a8d07-4ea6-40fb-855c-25b885902cfb)



![Screenshot 2024-06-09 at 7 39 45 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/5f87787b-3c51-4a18-bdc0-22d3ad9bacf2)












Administrator account
Create a username and password for virtual machine
IMPORTANT NOTE: These credentials will be used to log into the virtual machine (Keep them handy)

Inbound port rules
Public inbound ports: Allow RDP (3389)







Disable VM Firewall:
o Disable all firewalls in the VM to expose it globally.
o This allows recording of login attempts.
3. Deploy a Log Analytics Workspace:
o Create a log analytics workspace (e.g., “honeypot-logs”).
o Enable data collection from the VM into this workspace.

![Screenshot 2024-06-09 at 7 46 33 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/d2379d51-5046-4c33-a418-7187f075325d)



![Screenshot 2024-06-09 at 7 46 15 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/1e8aee73-4859-4ff0-b0d6-53d2586d319f)







Disks
Leave all defaults
Select Next : Networking >
Networking
Network interface
NIC network security group: Advanced > Create new
A network security group contains security rules that allow or deny inbound network traffic to, or outbound network traffic from, the virtual machine. In other words, security rules management.

Remove Inbound rules (1000: default-allow-rdp) by clicking three dots
Add an inbound rule
Destination port ranges: * (wildcard for anything)
Protocol: Any
Action: Allow
Priority: 100 (low)
Name: Anything (ALLOW_ALL_INBOUND)
Select Review + create





![Screenshot 2024-06-09 at 7 47 20 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/1835c084-4fc8-44a0-8c56-0549e02ca4a5)





Create a Log Analytics Workspace
Search for "Log analytics workspaces"
Select Create Log Analytics workspace
Put it in the same resource group as VM (honeypotlab)
Give it a desired name (honeypot-log)
Add to same region (East US 2)
Select Review + create






![Screenshot 2024-06-09 at 7 49 12 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/dbda55b0-d00f-431c-8986-fc545b289a7a)










It should look like this once it’s being deployed



![Screenshot 2024-06-09 at 7 49 46 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/b9726f7e-2ee7-461a-bc08-27a225b86c52)




![Screenshot 2024-06-09 at 7 49 46 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/9373762a-b9e5-429c-8b34-5953a83dea27)










Get API key from Geolocation 

Copy API key once logged in and paste into script line 2:($API_KEY = "<API key>"
Hit Save
Run the PowerShell ISE script (Green play button) in the virtual machine to continuously produce log data
Make an account with Free IP Geolocation API and Accurate IP Lookup Database
This account is free for 1000 API calls per day. Paying 15.00$ will allow 150,000 API calls per month.


<img width="827" alt="apikeyfromipgeolo" src="https://github.com/tw181802/Cyber-Course/assets/106920505/7cc3ca59-34ef-4663-bdc1-3434352f899d">





Scripting the Security Log Exporter
In VM open Powershell ISE
Set up Edge without signing in
Copy Powershell script into VM's Powershell (Written by Josh Madakor)
Select New Script in Powershell ISE and paste script
Save to Desktop and give it a name (Log_Exporter)


<img width="772" alt="splitpanes" src="https://github.com/tw181802/Cyber-Course/assets/106920505/227126c8-f703-4036-9e3c-ec0a5c855901">





Alternatively you can create your own script following these steps (OPTIONAL):
.Collecting Failed Login Attempts with PowerShell

Create/Use a PowerShell Script to Parse Logs:
o Open PowerShell ISE or any text editor.(link here for script)
o Write a script that queries the Security event log for failed login attempts.
o Extract relevant information such as account names and IP addresses.
o Here’s a sample script:
2. ($events = Get-WinEvent -LogName Security | Where-Object { $_.Id -eq
4625 }
3. foreach ($event in $events) {
4. $time = $event.TimeCreated
5. $account = $event.Properties[5].Value
6. $ipAddress = $event.Properties[19].Value
7. Write-Host &quot;Failed login attempt at $time from account $account
(IP: $ipAddress)&quot;
8. } )
9. Schedule Script Execution:
o Save the script as a .ps1 file.
o Schedule it to run periodically (e.g., every hour) using Task Scheduler.
o The script will collect data on failed login attempts.
10. Analyze the Data:
o Use the collected information to identify patterns.
o Map IP addresses geospatially to locate potential adversaries.
Correlate login attempts with other security events.
 Copy and paste key (with your API key
from ipgeolocation.io).
o Run the script to collect real data on login attempts.
View Login Attempts:
o In Event Viewer, under Windows Log, check the Security section.
o You’ll see login attempts from various locations.






Configure Microsoft Defender for Cloud
Search for "Microsoft Defender for Cloud"
Scroll down to "Environment settings" > subscription name > log analytics workspace name (log-honeypot)




![Screenshot 2024-06-09 at 7 55 36 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/8515904b-06ce-44e0-a876-d59cbee0060e)








Settings | Defender plans
Cloud Security Posture Management: ON
Servers: ON
SQL servers on machines: OFF
Hit Save





![Screenshot 2024-06-09 at 7 56 26 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/77a63d40-9c93-43bb-bd38-0234b53511c4)









Connect Log Analytics Workspace to Virtual Machine
Search for "Log Analytics workspaces"
Select workspace name (log-honeypot) > "Virtual machines" > virtual machine name (honeypot-vm)
Click Connect




![Screenshot 2024-06-09 at 7 57 55 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/a6f8089d-38f2-4402-8d01-68f6b31a28c2)










Connect VM to Microsoft Sentinel:
o Search for “Microsoft Sentinel” and create a new instance.
o Select the log analytics workspace you created.
o The VM should now be connected




Configure Microsoft Sentinel
Search for "Microsoft Sentinel"
Click Create Microsoft Sentinel
Select Log Analytics workspace name (honeypot-log)
Click Add



![Screenshot 2024-06-09 at 7 59 53 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/a9e9fd04-6e63-47d4-85ae-7c29930ffea8)



![Screenshot 2024-06-09 at 8 01 42 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/58ae1ab7-e800-4b9f-bd87-ed082ca734c5)





I’m remoting into the PC w/ the IP address above



<img width="897" alt="vmlogin" src="https://github.com/tw181802/Cyber-Course/assets/106920505/d1b5f623-941a-4239-9b84-3fd5dd2d5a69">



<img width="932" alt="eventlogandefenderoff" src="https://github.com/tw181802/Cyber-Course/assets/106920505/b32d3cc3-e568-4552-9569-11313aa06949">







I can’t ping the PC by IP address b/c the Firewall is enabled ( as you can see “Request timeout”)

![Screenshot 2024-06-13 at 7 43 49 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/d03fd311-31af-492a-98bb-a359e575658f)




*****I just disabled the Firewall

Disable the Firewall in Virtual Machine
Go to Virtual Machines and find the honeypot VM (honeypot-vm)
By clicking on the VM copy the IP address
Log into the VM via Remote Desktop Protocol (RDP) with credentials from step 2
Accept Certificate warning
Select NO for all Choose privacy settings for your device
Click Start and search for "wf.msc" (Windows Defender Firewall)
Click "Windows Defender Firewall Properties"
Turn Firewall State OFF for Domain Profile Private Profile and Public Profile
Hit Apply and Ok
Ping VM via Host's command line to make sure it is reachable ping -t <VM IP>



<img width="580" alt="firealloff" src="https://github.com/tw181802/Cyber-Course/assets/106920505/c1c1cd9a-d48f-4885-962f-5b9eeaef0351">





Now I can ping the PC w/ the IP Address

![Screenshot 2024-06-09 at 8 11 15 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/8aacfc1c-57b0-4977-a361-67b36b2c20d3)



Query the logs now


![Screenshot 2024-06-09 at 9 11 04 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/fe468ed8-2661-430d-b760-0db03e9b4d92)


Go to Tables to see the logs created


![Screenshot 2024-06-09 at 9 20 24 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/fe1289d7-74bc-4df5-852f-836b083828b0)




Create Custom Log in Log Analytics Workspace
Create a custom log to import the additional data from the IP Geolocation service into Azure Sentinel
Search "Run" in VM and type "C:\ProgramData"
Open file named "failed_rdp" hit CTRL + A to select all and CTRL + C to copy selection
Open notepad on Host PC and paste contents
Save to desktop as "failed_rdp.log" (or whatever you want)
In Azure go to Log Analytics Workspaces > Log Analytics workspace name (honeypot-log) > Custom logs > Add custom log
Sample
Select Sample log saved to Desktop (failed_rdp.log) and hit Next
Record delimiter
Review sample logs in Record delimiter and hit Next
Collection paths
Type > Windows
Path > "C:\ProgramData\failed_rdp.log"
Details
Give the custom log a name and provide description (FAILED_RDP_WITH_GEO) and hit Next
Hit Create




![Screenshot 2024-06-09 at 9 26 12 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/aab95bef-5b7f-4025-b715-e6a43ecbe805)








Query the Custom Log
In Log Analytics Workspaces go to the created workspace (honeypot-log) > Logs
Run a query to see the available data (FAILED_RDP_WITH_GEO_CL) NOTE:yours may be different

May take some time for Azure to sync VM and Log Analytics (NEW CHANGES) use this query below:
(<Logname>
| parse RawData with * "latitude:" Latitude ",longitude:" Longitude ",destinationhost:" DestinationHost ",username:" Username ",sourcehost:" Sourcehost ",state:" State ", country:" Country ",label:" Label ",timestamp:" Timestamp 
| extend EventCount = 1
| summarize event_count = sum(EventCount) by Sourcehost, Latitude, Longitude, Country, Label, DestinationHost
| project Latitude, Longitude, DestinationHost, Sourcehost, Country, Label, event_count)


![Screenshot 2024-06-11 at 6 18 51 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/30c61c36-648e-4064-899d-e4e45d35a13b)





Type in your log name and you’ll see ingested logs make sure to highlight the name and set the right time range

![Screenshot 2024-06-11 at 6 32 02 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/f5e9a377-8ec1-4f81-8e0c-a19c326ea714)



To Map Data Go To:

Sentinel > New Workbook 

![Screenshot 2024-06-11 at 6 48 44 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/6630196c-7ce1-427b-8872-632d5cf7a7a6)


![Screenshot 2024-06-11 at 6 54 32 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/e43497e3-251f-453c-a820-fc63f2868f59)




Display Data on a World Map:
o Use the collected data to map brute force attempts.
o Create workbooks in Microsoft Sentinel to visualize the data geospatially.
Remember to document your steps and share your experience with the community

To Map Data Go To:

Sentinel > New Workbook 

![Screenshot 2024-06-12 at 4 35 48 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/8eb3898f-8f48-4954-b906-c45089c544af)



Map Data in Microsoft Sentinel
Go to Microsoft Sentinel to see the Overview page and available events
Click on Workbooks and Add workbook then click Edit
Remove default widgets (Three dots > Remove)
Click Add > Add query
Copy/Paste the following query into the query window and Run Query

```
(FAILED_RDP_WITH_GEO_CL | summarize event_count=count() by sourcehost_CF, latitude_CF, longitude_CF, country_CF, label_CF, destinationhost_CF
| where destinationhost_CF != "samplehost"
| where sourcehost_CF != "")
```

Kusto Query Language (KQL) - Azure Monitor Logs is based on Azure Data Explorer. The language is designed to be easy to read and use with some practice writing queries and basic guidance.

Once results come up click the Visualization dropdown menu and select Map
Select Map Settings for additional configuration
Layout Settings
Location info using > Latitude/Longitude
Latitude > latitude_CF
Longitude > longitude_CF
Size by > event_count
Color Settings
Coloring Type: Heatmap
Color by > event_count
Aggregation for color > Sum of values
Color palette > Green to Red
Metric Settings
Metric Label > label_CF
Metric Value > event_count
Select Apply button and Save and Close
Save as "Failed RDP World Map" in the same region and under the resource group (honeypotlab)
Continue to refresh map to display additional incoming failed RDP attacks
NOTE: The map will only display Event Viewer's failed RDP attempts and not all the other attacks the VM may be receiving.




You can copy the query below since Azure recently changed and no longer have the FIELD Parse option and change the beginning part to your log name ex. THIS_WILL_BE_YOUR_LOG_NAME_CL


```

   (   FAILED_LOG_GEO_LC_CL
 |extend username = extract(@"username:([^,]+)", 1, RawData),
         timestamp = extract(@"timestamp:([^,]+)", 1, RawData),
         latitude = extract(@"latitude:([^,]+)", 1, RawData),
         longitude = extract(@"longitude:([^,]+)", 1, RawData),
         sourcehost = extract(@"sourcehost:([^,]+)", 1, RawData),
         state = extract(@"state:([^,]+)", 1, RawData),
         label = extract(@"label:([^,]+)", 1, RawData),
         destination = extract(@"destinationhost:([^,]+)", 1, RawData),
         country = extract(@"country:([^,]+)", 1, RawData)
 |where destination != "samplehost"
 |where sourcehost != ""
 |summarize event_count=count() by timestamp, label, country, state, sourcehost, username, destination, longitude, latitude)

```










World map of incoming attacks after 24 hours (built custom logs including geodata)



You can copy this query but change FAILED_LOG_GEO_LC_CL to your individual log name

```
FAILED_LOG_GEO_LC_CL
 |extend username = extract(@"username:([^,]+)", 1, RawData),
         timestamp = extract(@"timestamp:([^,]+)", 1, RawData),
         latitude = extract(@"latitude:([^,]+)", 1, RawData),
         longitude = extract(@"longitude:([^,]+)", 1, RawData),
         sourcehost = extract(@"sourcehost:([^,]+)", 1, RawData),
         state = extract(@"state:([^,]+)", 1, RawData),
         label = extract(@"label:([^,]+)", 1, RawData),
         destination = extract(@"destinationhost:([^,]+)", 1, RawData),
         country = extract(@"country:([^,]+)", 1, RawData)
 |where destination != "samplehost"
 |where sourcehost != ""
``` |summarize event_count=count() by timestamp, label, country, state, sourcehost, username, destination, longitude, latitude )

```

Custom Powershell script parsing data from 3rd party API (This is extracting the failed login attempts and ingesting them into the logs, Keep it running)







![Screenshot 2024-06-12 at 4 53 25 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/397c9c4f-9fa6-4220-8d69-77bdfeb103b7)



Lastly: Deprovision Resources
VERY IMPORTANT - Do NOT skip!

Search for "Resource groups" > name of resource group (honeypotlab) > Delete resource group
Type the name of the resource group ("honeypotlab") to confirm deletion
Check the Apply force delete for selected Virtual machines and Virtual machine scale sets box
Select Delete
![Screenshot 2024-06-12 at 4 56 45 PM](https://github.com/tw181802/Cyber-Course/assets/106920505/300b3dfc-8a10-4b9d-b6c9-6eb379565235)



If resources are not deleted they will eat up the free credits and fees may start to accumulate.



Remember to adapt the script to your specific use case and document your findings.
Happy hunting!

