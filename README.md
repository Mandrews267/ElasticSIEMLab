<h1>Elastic Stack Security and Event Management Home Lab</h1>


<h2>Description</h2>
In this lab, I will demonstrate how you can set up a SIEM home lab using Oracle’s VMWare VirtualBox that is operating a Kali Linux virtual machine (VM) with an Elastic reporting agent installed on the VM.  There are a few steps in completing this, with the first one is to download and install the VirtualBox hypervisor and Kali Linux and install that on the Hypervisor.  Once this is completed, you are ready to move forward to creating the Elastic SIEM.  
<br/>

<h2>Environments and Utilities Used</h2>

- <b>Oracle VirtualBox Hypervisor</b> 
- <b>Kali Linux</b>
- <b>Linux Command Line</b>
- <b>Elastic Stack</b>
<br/>

<h2>Major Project Tasks</h2>

- <b>Set up an Elastic Account.</b>
- <b>Download and install Oracle VirtualBox Manager hypervisor and Kali Linux</b>
- <b>Configure the Elastic Agent on the Linux VM to collect the log data and forward it to the SIEM</b>
- <b>Generate Security Events on the Kali VM</b>
- <b>Query to find the security events on the Elastic SIEM</b>
- <b>Create a dashboard to visualize security events</b>
- <b>Create alerts for security events</b>
<br/>

<h2>Task walk-through:</h2>

<h3>Task 1: Set up an Elastic Account</h3>
<ol>
  <li>Sign up for a free 14-day trial account to use Elastic Cloud at: <a href="https://cloud.elastic.co/registration">https://cloud.elastic.co/registration</a>.</li>
  <p align="center">
 
   <div>
     <img src="https://i.imgur.com/xh60I2l.png" alt="Elastic SIEM Welcome Page">
   </div>
   
 <br>
    <p>During the registration process, the application service asks a few questions about what you are wanting to use the Elastic platform for. We are using it for SIEM monitoring, so select the security tab on the right side of the screen.  They will also request a region for the cloud service to be deployed from, I would select the one they recommend as this is for experimental use at this time.  This will automatically generate the first Elastisearch deployment, which will be the one that will be used for the data collection.</p>

 <li>After registering your Elastic account, log into the Elastic Cloud console at: <a href="https://cloud.elastic.co">https://cloud.elastic.co</a>.</li> 
 <br>
<div>
  <img src="https://i.imgur.com/lDuTq2O.png" alt="Elastic Cloud Deployment Page"/>
</div>
<br>
<p>When you reach this point, you will have created your Elastic account and begun your free trial.  The deployment, "My Deployment" will be displayed and to enter your deployment you will click on the name.  I recomend that familiarizing yourself with the layout of the different areas of the application first before you start using, as navagating the different areas effectively is a large part of being successful in using this tool.</p>
</ol>
</p>
<h3>Task 2: Setting up the Linux VM</h3>
<p>Next, we set up a Linux virtual machine.  There are many Linux distributions, and you can select any one of the as well as any hypervisor.  I selected to use Oracle VirtualBox as my hypervisor and Kali Linux as that is the distro I am most familiar with.  Since some individuals may not have experience with setting up virtual environments, I have provided the steps that need to be completed to create the Linux virtual machine on a Windows OS host system below.</p>
<b>Follow the following steps to create the virtual machine:</b>
<br>
<ol>
  <li>Go to <a href="https://www.virtualbox.org">https://www.virtualbox.org</a> and select the download button.  This will take you to a page with different packages you can download for different host OS’s.  I selected Windows hosts as that is what I am using as my host OS.  Once this is downloaded, open the location in your file manager and double click to begin the installation.  This was located in my downloads folder as shown below.</li>
  <br>
  <div>
    <img src="https://i.imgur.com/WSbd3oc.png" alt="VirtualBox Download"/>
  </div>
  <br>
  <li>Double click on the application listing in the download folder and start the setup wizard to install the hypervisor</li>
  <li>Download a Kali Linux VM from the official Kali Linux website at: <a href="https://www.kali.org/get-kali/#kali-virtual-machines">https://www.kali.org/get-kali/#kali-virtual-machines</a>.  Select the option that correlates with whichever virtualization application you are using to deploy the VM with.  </li>
  <br>
  <div>
    <img src="https://i.imgur.com/GhsPpWH.png" alt="Kali Linux Download"/>
  </div>
  <br>
  <li>Once downloaded, open VirtualBox and select the “Add” option at the top of application to begin installation of the Linux VM.</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/2pfGYaQ.png" alt="VirtualBoxManager"/>
  </div>
  <br>
  <li>Go to your download folder and transfer the compressed file to a location on your PC where you want to store the Linux VM and unzip the file. Inside the unzipped folder, you will find two items, with the first item being a VirtualBox Machine Definition and the other being a Virtual Disk Image.  You will want to select the VirtualBox Machine Definition file as noted in the image below.</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/rQ0MSDT.png" alt="VM File"/>
  </div>
  <br>
  <li>Once the installation is completed, click on settings to verify the setup is completed correctly, specifically looking at the number of CPU’s that are being used, amount of memory committed to be used by the VM and allocated space for the hard drive is what is desired.  You may also want to update the general settings under the advanced tab to share copy and paste functions from your host system to the virtual system.  This is completed by changing the setting for “Shared Clipboard” and “Drag’n’Drop” to Bidirectional.  If you are hosting multiple VM’s you will also want to make sure you enter a name for the machine on the basic tab under general settings.  Upon completion of the settings, the machine is now ready to be turned on, which can be completed a couple of different ways; click on the start button at the top of hypervisor or right click on the machine you want to start up and select start.  You can also double click on the machine you want started and it will also begin.  The default username and password login for Kali Linux “kali” for both.</li>
  <br>
  <p><b>*NOTE*:</b>If there are issues with setting up the hypervisor and VM, there are multiple YouTube tutorials and resources / documentation at the respective websites that can assist in answering questions and troubleshooting various issues.</p>
</ol>





<p align="center">
Launch the utility: <br/>
<img src="https://i.imgur.com/62TgaWL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
