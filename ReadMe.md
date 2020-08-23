#### **Step 1**
Login to the environment with the following credentials:
  >username:  administrator@corp.local  
  password:  VMware1!
  
  
#### **Step 2**
1. Login to vCenter. Select the "Use Windows Credentials" option.
2  Power on the VM titled "tkgimc-01a"

#### **Step 3 - SSH to VPOD Router and Add Routes**
On the desktop there is an app called "MTPutty".  Open this app and double-click on "vPOD Router (192.168.100.1).  This should bring up an SSH to the vPod router.  The vPod router is like the data-center core router.  The NSX T0 router (which is already provisioned) peers with it.  We need to add some static routes on the vPod router.  At the command prompt type the following commands (when prompted for a password, use "VMware1!"):

  >telnet localhost 2601  
  en 
  config t
  ip route 10.10.80.0/24 192.168.210.3  
  ip route 10.10.90.0/24 192.168.210.3  
  exit  
  copy run start  
  

  
  
2.  
1.  add default static route on T0 pointing to 192.168.210.1
2.  add static routes on vpod router:
root@vPodRouter-HOL:~# ip route add 10.100.100.0/24 via 192.168.210.1
root@vPodRouter-HOL:~# ip route add 10.200.200.0/24 via 192.168.210.1
root@vPodRouter-HOL:~# ip route add 172.31.0.0/24 via 192.168.210.1
3.  add VIP pool in NSX for 10.100.100.0/24
4.  add DNS entries for opsman, tkgi-api, and harbor
(opsman originally set for 10.40.14.34)


8: eth1.210@eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1600 qdisc noqueue state UP
    link/ether 00:50:56:26:86:bc brd ff:ff:ff:ff:ff:ff
    inet 192.168.210.1/24 brd 192.168.210.255 scope global eth1.210
    inet6 fe80::250:56ff:fe26:86bc/64 scope link
       valid_lft forever preferred_lft forever
