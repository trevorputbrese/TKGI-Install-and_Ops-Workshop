#### **Step 1**
1. Login to the environment with the following credentials:
    >username:  administrator@corp.local  
    password:  VMware1!
  
  
#### **Step 2**
1. Open the Chrome web browser
2. Login to vCenter (it's bookmarked). Select the "Use Windows Credentials" option.
3. Power on the VM titled "tkgimc-01a"

#### **Step 3 - SSH to VPOD Router and Add Routes**
1. On the desktop there is an app called "MTPutty".  Open this app and double-click on "vPOD Router (192.168.100.1).  This should bring up an SSH session to the vPod router.  The vPod router is like the data-center core router.  The NSX T0 router (which is already provisioned) peers with it.  We need to add some static routes on the vPod router.  
2. In the vPod Router SSH session, type the following commands (when prompted for a password, use "VMware1!"):

```
  telnet localhost 2601  
  en 
  config t  
  ip route 10.10.80.0/24 192.168.210.3  
  ip route 10.10.90.0/24 192.168.210.3   
  exit  
  copy run start  
```

#### **Step 4 - Add "TKGi Floating IP Pool" in NSX**
1.  Open up the Chrome web browser
2.  Login to NSX Manager (it's bookmarked).
3.  Click on the "Networking" tab at the top
4.  In the "Networking" screen, click on the "IP Address Pools" link near the bottom left.
5.  Select the "IP Pools" menu (NOT the "IP Blocks" menu) add click "Add".  
  a.  A screen should pop up that says "Add New IP Pool".  
  b.  Enter the following details:
        >Name:  Floating IP Pool  
  c.  Click the "+" sign under Subnets to add a new subnet.  
  d.  Enter the below details (you will need to click on the pencil icon in order to edit the details):  
        >IP Range:  10.10.90.2 - 10.10.90.254  
        CIDR:  10.10.90.0/24
        DNS Servers:  192.168.110.10  
        DNS Suffix:  corp.local  
        

  
#### **Step 5 - Add DNS Entries for TKGi Components**
1.  One the Windows Taskbar (the menu at the bottom of the screen) click on the search icon and type "DNS".  An option for the "DNS Desktop App" should pop up.  Click on that to open the DNS Server.
2.  Click on the drop-down arrow next to "ControlCenter.corp.local" to see the list of zones beneath it.
3.  Click on the drop-down arrow next to "Reverse Lookup Zones".
4.  Right click on "Reverse Lookup Zones" and select "Add Zone":
    a.  In the "New Zone Wizard" that pops up, click on "Next" four times until it prompts you for the "Network ID"
    b.  In the "Network ID" field type:  10.10.90
    c.  Click on "Next" twice and then "Finish".
3.  Back in the main "DNS Manager" window, click on the drop-down arrow next to "Forward Lookup Zones" to see the list of zones beneath it.
4.  Under "Forward Lookup Zones" you'll see a zone called "corp.local".  Right-click on "corp.local" and select (New A or AAAA) record.   
    a.  Create the following A records:
    >opsman     10.10.90.2  
    tkgi-api    10.10.90.5  
    harbor      10.10.90.6
 
