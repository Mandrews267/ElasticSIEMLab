<h1>Elastic Stack Security and Event Management Home Lab</h1>


<h2>Description</h2>
In this lab, I will set up a SIEM home lab using Oracle’s VMWare VirtualBox that is operating a Kali Linux virtual machine (VM) with an Elastic reporting agent installed on the VM.  There are a few steps in completing this, with the first one is to download and install the VirtualBox hypervisor and Kali Linux and install that on the Hypervisor.  Once this is completed, you are ready to move forward to creating the Elastic SIEM.  
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
  <br>
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
<h3>Task 2: Setting up the Linux VM</h3>
<p>Next, we set up a Linux virtual machine.  There are many Linux distributions, and you can select any one of the as well as any hypervisor.  I selected to use Oracle VirtualBox as my hypervisor and Kali Linux as that is the distro I am most familiar with.  Since some individuals may not have experience with setting up virtual environments, I have provided the steps that need to be completed to create the Linux virtual machine on a Windows OS host system below.</p>
<br>
<p><b>Follow the following steps to create the virtual machine:</b></p>
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
<h3>Task 3: Setting up the Agent to Collect Logs</h3>
<p>Agents are software programs that are installed on endpoints or any device you want to collect data from and send to a centralized system for analysis and monitoring.  With Elastic SIEM, the agent is used for collection and forwarding of security-related events from individual endpoints to Elastic SIEM instances.</p>
<br>
<ol>
  <li>Open a web browser and go to <a href="https://cloud.elastic.co">https://www.cloud.elastic.co</a> and log into Elastic.  Once logged in, select the deployment you created in the first task.  It should be noted under the “Hosted Deployments” and named “My deployment.”</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/CGwLUom.png" alt="My Deployment"/>
  </div>
  <br>
  <li>When you reach the next screen, you will go to the menu on the right side of the screen and at the bottom, expand the “Management” menu and select “Integrations.”  Once you reach this page, you will want to select “Elastic Defend”.  If it does not appear at the top of the integrations page, you can complete a search for it.</li>
   <br>
  <div align="center">
    <img src="https://i.imgur.com/h8KzLzC.png" alt="Creating Elastic Defend Integration"/>
  </div>
  <br>
  <li>Click on the “Elastic Defend” tab and select “Add Elastic Defend.” Click at the bottom of the page “Install Elastic Agent.”</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/r6IYlGV.png" alt="Install Elastic Agent"/>
  </div>
  <br>
  <li>The next page will provide installation instructions for various machine types that is to be run in the respective terminal.  If you are following along with me, you will want to make sure you copy the commands for the Linux machine type.</li>
   <br>
  <div align="center">
    <img src="https://i.imgur.com/DrNeqpf.png" alt="Install Elastic Agent2"/>
  </div>
  <br>
  <li>Paste the command into the Kali terminal (command line) and press enter to run the command.</li>
   <br>
  <div align="center">
    <img src="https://i.imgur.com/lOXojnl.png" alt="Install Elastic Agent Command Line"/>
  </div>
  <br>
  <li>You will then be asked enter the Sudo password for kali, which is kali and to confirm the location of where the Elastic Agent will be installed at and that it runs as a service.  Select “Y” for yes.  After completing this, you should receive a message of, “Elastic Agent has been successfully installed.”</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/zrGDLBe.png" alt="Install Elastic Agent Command Line2"/>
  </div>
  <br>
  <li>Once this is completed, you can verify that the agent has been installed by running the following command: sudo systemctl status elastic-agent.service. If there is an error in installing the agent, make sure the Kali VM is connected to the internet before proceeding by running a ping command of any website, such as google.com.</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/XERERAu.png" alt="Elastic Agent Status"/>
  </div>
  <br>
</ol>
<h3>Task 4: Generating Security Events on the Kali VM</h3>
<p>It is now time to verify that the agent is working correctly and this can be completed by generating some security-related events on the Kali VM.  Using a tool like Nmap (Network Mapper) is a good choice for this as it is an open-source utility that is used for network exploration, management, and security auditing.  Nmap is designed to discover hosts and services on a computer network by creating a “map” of the network.  It can be used to scan hosts for open ports, determine operating systems and software running on a target system, and gather other relevant system information about the network.</p>
<br>
<p><b>To run an Nmap scan, complete these steps:</b></p>
<br>
<ol>
  <li>Install Nmap on the Linux VM if you are not using Kali Linux distro.  Nmap is already installed with the Kali distribution.  Open a terminal and run the command: <b>sudo apt-get install nmap</b>.  This will complete the installation.  You can also check to see if it is already installed before downloading by running the command: <b>nmap –version</b> in the terminal.</li>
  <li>Run a scan on the Kali machine by running the command: <b>sudo nmap (vm-ip address)</b>.  A scan can also be run of your host machine if you place the Kali VM on a bridged network.  To make a change to a bridged network, you will need to make that change in the hypervisor network settings.  It probably is currently set to NAT (network address translation).</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/GKnKOn7.png" alt="Nmap scan"/>
  </div>
  <br>
  <li>The scan will generate multiple security events, such as the detection of any open ports and the identification of services running on those ports.  There a several more Nmap scans you can run to generate additional traffic and events. Below are a few and explinations as to how each of them work:</li>
  <br>
  <ul>
    <li>nmap -sS (ip address)</li>
      <ol>
        <li>The command sends a SYN packet to each port on the target system without completing the full TCP handshake.</li>
        <li>If a port is open on the target machine, it will respond with a SYN-ACK to the scanning machine.</li>
        <li>Instead of completing the connection with the target machine, Nmap sends a reset (RST) packet to drop the connection.</li>
        <li>If a port is closed, the target machine will respond with a RST packet.</li>
        <li>If the port is filtered by a firewall, you may not receive any response or an ICMP error.</li>
      </ol>
    <br>
    <li>nmap -sT (ip address)</li>
      <ol>
        <li>Attempts a full three-way handshake with each scanned port on target machine.</li>
        <li>Target machine sends a SYN packet to the target port.</li>
        <li>If the port is open, the target responds with a SYN-ACK.</li>
        <li>Nmap then completes the handshake with an ACK and immediately closes the connection with an RST.</li>
        <li>If the port is closed, the target responds with a RST.</li>
        <li>If the port is filtered (firewall in place), there may be no response or an ICMP error.</li>        
      </ol>
    <br>
    <li>nmap -p- (ip address)</li>
      <ol>
        <li>The -p- command tells Nmap to scan all TCP ports (1 - 65,535) on the target.</li>
        <li>It determines whether each port is open closed or filtered.</li>
        <li>This scan is used to discover for non-standard services running on unusual ports, identifying hidden services that wouldn't be detected in a default scan, and to perform a comprehensive security assessment on a target network.</li>
     </ol>
    <br>
    <li>nmap -A -sV localhost</li>
      <ol>
        <li>Performs an aggressive scan of the local machine that allows for OS and version detection, tracerroute, and script scanning.</li>
        <li>Scans for open ports on the host system.</li>
        <li>Performs tracerout to map network paths.</li>
        <li>Runs default NSE scripts, which may include security checks.</li>
      </ol>   
  </ul>
  <br>
  <p>The command run below is <b>nmap -A -sV localhost</b>.</p>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/3F4bzkS.png" alt="Nmap localhost scan"/>
  </div>
  <br>
</ol>
<h3>Task 5: Querying for Security Events in the Elastic SIEM</h3>
<p>Hopefully, we have been successful in forwarding data from the Kali VM to the SIEM, so we can start querying and analyzing the logs in the SIEM.</p>
<br>
<p><b>These are the steps you will want to follow to complete this:</b></p>
<br>
<ol>
  <li>You will now want to go to the Elastic deployment just created and view the data captured by the system from sending the nmap command.  This is completed by navigating to your deployment and selecting under the Security view “Discover” on the right menu.</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/McgaDVT.png" alt="Elastic Discover"/>
  </div>
  <br>
  <li>Once you enter the discover tab you are able to view captured data from the endpoint you created on the Kali machine.  In the view I am providing below, I have the Data view set to logs-*, which can also be set to many different view options.  I also completed a more detailed search by entering in “nmap” to filter any captured data that has nmap as part of its information.  You are also able to set a range of what data is captured, which can be customized to any time period.  The result of my search shows that data was captured that represents data generated from my command of sudo nmap -A -sV localhost, which can be seen below:</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/uBSMCqo.png" alt="nmap log capture"/>
  </div>
  <br>
  <li>The next thing that needs to be completed is to create a new “Solution View.”  This is completed by creating a new space in the Elastic platform.  This is completed by going to the left screen menu down to the “Management” and selecting “Stack Management”. Scroll down on the Stack Management menu and click on “Spaces”</li>
   <br>
  <div align="center">
    <img src="https://i.imgur.com/80qNXNw.png" alt="New Spaces"/>
  </div>
  <br>
  <li>After getting into the “Spaces” page, you are now able to create a new space.  You will want to create an Observability space when doing this.  This will allow for more detailed views of captured data.  Click on the top right button “Create space” to get started.</li>
   <br>
  <div align="center">
    <img src="https://i.imgur.com/q1eNemt.png" alt="Create Observability Space"/>
  </div>
  <br>
  <li>There are a few options that need to be filled out in this section such as Name, Description, and the important one is “Select Solution View.”  The dropdown menu provides four options, When the Elastic Instance was created in this lab, the “Security Solution View,” which we briefly viewed above.  We now want to create the “Observability” view.  Select this option, name your space, provide a description, and select an avatar if wanted.  When complete, click on apply change or save changes.</li>
   <br>
  <div align="center">
    <img src="https://i.imgur.com/Mp5g1E0.png" alt="Observability View"/>
  </div>
  <br>
  <li>Once this is completed, you will be sent back to the “Spaces” screen.  Select the Observability View.  You can toggle between the different views by clicking on the avatar icon at the top of the page.  Select the Observability View for the next steps.</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/pfHOIxz.png" alt="Spaces View"/>
  </div>
  <br>
  <li>Under the observability menu on the left of the screen, select the discover tab, which will take you to the log explorer.  You can sort the captured data here using process arguments by entering in the search bar process.args : “nmap”.  Make sure you have “All Logs” selected and you may need to extend the search time period to locate the previously entered nmap command.</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/FxJiOiD.png" alt="Observability Logs Explorer View"/>
  </div>
  <br>
  <li>You can open a more detailed view of the captured data packets by clicking on the diagonal arrows next to any individual instance that will reveal a multitude of data broken down into three sections, Overview, Table, and JSON.  The Overview is basic information of the data packet.  The Table provides finer details about the instance such as an event ID, event kind, timestamp, index and many other data points.  The JSON tab reveals a file of the data points associated with the particular instance and can be very useful in HTTP compression and data manipulation.</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/BR0BbOI.png" alt="Detailed Observability Logs"/>
  </div>
  <br>
</ol>
<h3>Task 6: Create a Dashboard to Visualize Events</h3>
<p>To create an actual SIEM, it is likely that you want to include visualizations as part of the deployment.  This allows SOC team members a valuable tool to easily analyze the logs and identify patterns or anomalies in the incoming data.  An example of this is to create a simple dashboard that shows a count of security events over time.</p>
<br>
<p><b>To create dashboards, follow the following steps:</b></p>
<br>
<ol>
  <li>Go to the top of the application and switch over from the “Observability” view to the “Security” view.</li>
  <br>
  <li>Click on the “Dashboards” tab and then select “Create Dashboard” on the right side of the screen.</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/oTuGQcu.png" alt="Create Data Visualization"/>
  </div>
  <br>
  <li>In the “Editing new dashboard” screen, you will want to select “Create visualization.”</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/xLaIChi.png" alt="Create Data Visualization"/>
  </div>
  <br>
  <li>To create the graph, you will need to set your horizontal or X axis and vertical or Y axis.  The horizontal axis should be the @timestamp and the vertical axis should be a count, which is a count of records for each recorded time segment.  This can be found on the right side of the screen.  Below is an image of the screen after I have selected the X and Y axis data points, showing that it automatically generates the visualization.   </li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/f9qtqXy.png" alt="Bar Chart Visualization"/>
  </div>
  <br>
  <li>Upon completion of setting up the respective axis, select “Save and return” at the top right of the screen, which returns you to a final save screen for the visualization.  Click on save again at the top right of the screen and provide a name, description, and tag if desired.  I highly recommend providing a title to make it easily recognized.  I noted my chart as “log Inflows.”  You can also hover over the graph and a pop-up will appear with a gear that allows you to edit settings and enter the title again, displaying it on the actual graph.</li>
  <br>
  <div align="center">
    <img src="https://i.imgur.com/992MY4a.png" alt="Log Inflow Graph"/>
  </div>
  <br> 
</ol>
<h3>Task 7: Create an Alert</h3>
<br>
<p>One of the reasons to use a SIEM is to allow for effective and efficient management of security events and the environments providing timely, accurate data to SOC analysts.  A well-managed SIEM can provide a tremendous advantage to a team.  Alerts are created based on predefined rules or custom queries, and can be configured to trigger specific actions when specific conditions are met.</p>
<br>
<p><b>Steps for creating an alert:</b></p>






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
