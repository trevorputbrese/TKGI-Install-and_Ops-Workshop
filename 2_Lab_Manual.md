## Lab Manual (Make sure you complete the prerequisite steps first)##

#### **Step 1 - Login to the TKGI-MC and Launch the Install Wizard####
1.  Launch the Chrome web browser and open up the TKGI Management Console web page (it is bookmarked "TKGIMC" in the bookmarks bar).
1.  Login with the following credentials:
    >username:  root  
    password:  VMware1!
2.  You shoud see a welcome screen with two options:  Install and Upgrade.  Select the "Install" option.
3.  On the next screen select the "Import Configuration File".  We are going to import a templated configuration file and customize it.
4.  Click on the option to "Browse".  This should bring up a Windows file explorer menu in E:/Downloads
5.  In the E:/Downloads folder select the file named **PksConfiguration (BYOT).yaml** and click "Open".
6.  **DO NOT CLICK APPLY CONFIGURATION**  Click on the **Edit in Wizard** option
 
  
#### **Step 2 - Review and Edit the Install Parameters**
1.  We will review the installation wizard together and edit several values before applying.  The following values need to be edited.
2.  Click on the "Next" button to bring up the "Networking" Menu
3.  Under Network Resources, for "Floating IP Pool ID", select the "Floating IP Pool" you created in the pre-requisite steps (it should be simply called "Floating IP Pool")
4.  Select tickbox next to "Disable SSL Certificates Validation"
5.  Click on the "Next button" to bring up the "Identity" Menu
6.  Change the TKGI API FQDN value to "tkgi-api.corp.local".  This should be the same domain name for which you created a DNS entry in the pre-requisite steps.

