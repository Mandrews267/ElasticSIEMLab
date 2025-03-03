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
  <li>Sign up for a free 14-day trial account to use Elastic Cloud at <a href="https://cloud.elastic.co/registration">https://cloud.elastic.co/registration.</a></li>
  <p align="center">
   
    
</ol>
<p>Let this be the first paragraph of information</p>
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
