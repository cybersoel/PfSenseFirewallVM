<h1 align="center">Summary Diagram</h1>


<p align="center">
<br/>
<img width="500" alt="Portfolio" src="https://i.imgur.com/DNU6rmW.png">
<br />
</p>


<br />
<br />

<h1 align="center">Project walk-through</h1>

<br />
<br />

---
<a name="toc"></a>
**Table of Contents:**

- [Downloading pfSense file](#downloading-pfsense-file)
- [pfSense VM configuration](#pfsense-vm-configuration)
- [pfSense Installation](#pfsense-installation)
- [pfSense Network Interface Setup](#pfsense-network-interface-setup)
- [pfSense Web Interface Setup](#pfsense-web-interface-setup)
- [Understanding Key Firewall Rule Parameters](#understanding-key-firewall-rule-parameters)
- [Identifying the target website's IP address](#identifying-the-target-websites-ip-address)
- [Creating an Alias](#creating-an-alias)
- [Creating a Blocking Rule](#creating-a-blocking-rule)
- [Creating an Allow-all Rule](#creating-an-allowall-rule)
- [Host Network Configuration](#host-network-configuration)
- [Changing Host's Default Gateway](#changing-hosts-default-gateway)
- [Testing the rules](#testing-the-rules)



---

<h4>Tip: Any configuration options not mentioned in the walkthrough can be left at their default settings</h4>

---



[back to top](#toc)
## Downloading pfSense file

<br />
<br />

 - Download the pfSense ISO file.
   - Visit the official pfSense website (https://www.pfsense.org/download/)
   - Alternatively, use this direct link to bypass data collection: https://repo.ialab.dsu.edu/pfsense/
     - *Choose the latest version.iso.gz file*
     - *After downloading, extract the file using 7-Zip or a similar tool*

<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/fHSWBFw.png">
<br />
<br />
<br />
<br />

---
[back to top](#toc)
## pfSense VM configuration

<br />
<br />


 - Launch VMware Workstation or VMware Player
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/uDO11Aq.png">
<br />
<br />
<br />
<br />

 - Create a new virtual machine:
   - Select "Custom (advanced)" setup
   - Choose "I will install the operating system later"
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/oMng2lp.png">
<br />
<br />
<br />
<br />

 - Configure the guest OS:
   - Select "Other" as the operating system
   - Choose "FreeBSD 64-bit" as the version
   - Allocate resources *(In this lab we only need the VM to have minimum performance!)*
     - *1 GB RAM*
     - *1 core processor*
     - *20 GB virtual hard disk*
   - Use default settings for other options
<p align="center">
<br/>
<img width="480" alt="Portfolio" src="https://i.imgur.com/gVvqTdN.png">
<br />
<br />
<br />
<br />

 - Edit virtual machine settings:
   - Navigate to the CD/DVD section
   - Select "Use ISO image file" and browse to the extracted pfSense ISO
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/OzPUwj8.png">
<br />
<br />
<br />
<br />

 - Configure network settings:
    - Change the network adapter from NAT to "Bridged" *(This allows the pfSense VM to obtain its own IP address on your network)*
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/55Cq8Ba.png">
<br />
<br />
<br />
<br />


---
[back to top](#toc)
## pfSense Installation

<br />
<br />


 - Power on the virtual machine
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/g89VsPr.png">
<br />
<br />
<br />
<br />


 - Accept default options (the first row options) throughout the installation process
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/teO8jSL.png">
<br />
<br />
<br />
<br />


 - when you see a screen like below:
    - Press the spacebar to select all(*)
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/YCGvcHf.png">
<br />
<br />
<br />
<br />

 - Choose "Yes" to destroy the current contents of the disk
 - Allow the installation to complete and the VM to reboot

<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/IQdONuX.png">
<br />
<br />
<br />
<br />

---
[back to top](#toc)
## pfSense Network Interface Setup

<br />
<br />


 - VLAN configuration:
    - When asked "Should VLANs be set up now?", type "n" for no
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/ij7Zqwg.png">
<br />
<br />
<br />
<br />

 - Interface assignment:
    - For WAN interface, type "em0" (visible in the Valid interface options at the top of your screen)
    - For LAN interface, press Enter to skip (we'll use only one interface for this setup)
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/3m5FpSS.png">
<br />
<br />
<br />
<br />


 - Remember the assigned IP address:
    - You should see the em0 interface configured with an IP (e.g., 192.168.1.185/24)
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/xMBhgCH.png">
<br />
<br />
<br />
<br />

---
[back to top](#toc)
## pfSense Web Interface Setup

<br />
<br />



 - Accessing the pfSense web interface:
    - Open a web browser on your host machine
    - browse the IP address (em0 interface) we configured perviously 
    - We will use pfSense default login credentials:
     - *Username: admin*
     - *Password: pfsense*

<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/FNYQ7hn.png">
<br />
<br />
<br />
<br />

 - pfSense setup wizard:
    - Click "Next" to start the configuration process
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/J5m8aCo.png">
<br />
<br />
<br />
<br />

 - General Information:
    - Set Hostname: "pfSenseLab"
    - Set Domain: "localdomain"
    - Primary & Second DNS Server: 8.8.8.8 (Google's public DNS)
<p align="center">
<br/>
<img width="540" alt="Portfolio" src="https://i.imgur.com/PSsa1JD.png">
<br />
<br />
<br />
<br />


 - Time server configuration:
    - Leave default NTP servers or add your preferred time servers

<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/FXTXVDx.png">
<br />
<br />
<br />
<br />


 - WAN Interface Configuration:
    - Configure a static IP for the firewall
    - Use the IP address from the URL bar
    - Set the upstream gateway to your home router's IP (typically ends with .1)
     - *Tip: Check your host computer's default gateway to confirm the router IP*


<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/UBoQt71.png">
<br />
<br />
<br />
<br />

 - Set the admin password *(Make sure you don't forget!)*

<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/N3aAMlm.png">
<br />
<br />
<br />
<br />


 - Now let's go to the pfsense web console main page Dashboard. We can see our firewall information such as : interfaces, system, uptime, and resource usage.
<p align="center">
<br/>
<img width="540" alt="Portfolio" src="https://i.imgur.com/DQjUHSQ.png">
<br />
<br />
<br />
<br />

---
[back to top](#toc)
## Understanding Key Firewall Rule Parameters


<br />
<br />


 - Let's make a new firewall rule! Navigate to Firewall > Rules
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/K1tY1ui.png">
<br />
<br />
<br />
<br />



 - Click ADD at the bottom of the screen. You will see many firewall options that can be configured. We will learn what each section means.
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/tt51UUx.png">
<br />
<br />
<br />
<br />



 - Action: Our firewall rule can take three actions against specified network traffic:
    - Pass: Allow traffic
    - Block: Silently drop traffic
    - Reject: Drop traffic and notify the source
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/CE8SJXK.png">
<br />
<br />
<br />
<br />



 - "Disabled" checkbox allows you to create inactive rules for future use
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/NMNDPVo.png">
<br />
<br />
<br />
<br />


 - Interface: We can choose which network interface the rule applies to (e.g., WAN, LAN). For this walkthrough, we only have a WAN interface configure. 
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/qKGuOxK.png">
<br />
<br />
<br />
<br />


 - Address Family: We can select either IPv4, IPv6, or both for rule application
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/egtFHS2.png[">
<br />
<br />
<br />
<br />


- Protocol: Specify which protocol(s) the rule affects (e.g., TCP, UDP, ICMP, or Any)
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/AvbnDYI.png">
<br />
<br />
<br />
<br />

 - Source: The source of the network connection to which the rule will apply. For example, if we wanted to block connections to Facebook from this network, the source value would be 192.168.1.0/24, with a destination value of Facebook's IP range.
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/yCmaXKl.png">
<br />
<br />
<br />
<br />


 - Destination: Specify the target of traffic the rule will match. See the example under the Source heading to understand what this means.
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/Np1u3IZ.png">
<br />
<br />
<br />
<br />

 - Logging options: We can enable logging to track when the rule is triggered. It is useful for monitoring and troubleshooting
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/7ecaTCJ.png[">
<br />
<br />
<br />
<br />


 - Rule description: We can add a clear, concise description to help manage and understand rules
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/1asDdqO.png">
<br />
<br />
<br />
<br />


---
[back to top](#toc)
## Identifying the target website's IP address

<br />
<br />

 - Since now we understand the basics of setting up a firewall rule, let's make a rule that blocks any host in our network connecting to a specific domain.
    - Open a command prompt on your host machine
    - Use `ping example.com` to get the IP address of the site you want to block
    - Note down the IP address.

<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/Te89Q9P.png">
<br />
<br />
<br />
<br />


---
[back to top](#toc)
## Creating an Alias

<br />
<br />

 - Aliases group IPs, networks, or ports for rule management. Aliases make our lives easier. Instead of remembering IP addresses or port numbers, we can simply reference an alias we’ve created.
 - Go to Firewall > Aliases
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/xeAsa71.png">
<br />
<br />
<br />
<br />


 - We will create an Alias for the target website we want to block and use it as the source or destination within firewall rules. Name the Alias and enter the IP address we retrieved from pinging the website.
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/oQxNm90.png">
<br />
<br />
<br />
<br />


---
[back to top](#toc)
## Creating a Blocking Rule

<br />
<br />

 - Navigate to Firewall > Rules, then click "Add" to create a new rule. Configure as follows:
    - Action: Block
    - Interface: WAN
    - Protocol: Any
    - Source: Any (192.168.1.0/24)
    - Destination: Select your newly created alias
 - Save the rule

<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/znR1Eue.png">
<br />
<br />
<br />
<br />


---
[back to top](#toc)
## Creating an Allow-all Rule

<br />
<br />

We need to add one more rule to complete our firewall configuration. Currently, we have two rules in place: our custom rule blocking traffic to Example.net, and pfSense's built-in default rule that blocks all traffic. Firewalls process rules from top to bottom, applying the first matching rule to each packet. By adding an "Allow All" rule at the bottom, we create a logical flow:

<br />

 - First, the firewall checks if the traffic is destined for Example.net and blocks it if so.
 - If the traffic isn't going to Example.net, it moves to the next rule, which allows everything else.

<br />

This setup effectively blocks only Example.net while permitting all other traffic, giving us the selective control we want over our network.

<br />
<br />

 - Navigate to Firewall > Rules, then click "Add" to create a new rule.
    - Add another rule below the blocking rule
    - Set Action to "Pass" and leave other options as "Any"
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/Cb44JLX.png">
<br />
<br />
<br />
<br />




 - Ensure the block rule is above the allow-all rule. Use the arrow buttons to adjust if necessary

<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/OS3qxNR.png">
<br />
<br />
<br />
<br />



 - Click "Apply Changes" at the top of the page
<p align="center">
<br/>
<img width="680" alt="Portfolio" src="https://i.imgur.com/qzyLdb6.png">
<br />
<br />
<br />
<br />

---
[back to top](#toc)
## Host Network Configuration




 - Let's examine our host computer's current network configuration. Open a command prompt on your machine and type `ipconfig /all`. 
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/KEKaJGz.png">
<br />
 
Currently, the host machine is communicating directly with the router. Our goal is to redirect this traffic through our pfSense firewall.


<br />
<br />
<br />
<br />

 - To help you understand, I've created a diagram:

<p align="center">
<br/>
<img width="500" alt="Portfolio" src="https://i.imgur.com/TMJsTNr.png">
<br />
<br />
<br />
<br />

---
[back to top](#toc)
## Changing Host's Default Gateway

<br />
<br />


 - Press Win+R, type `ncpa.cpl`, and press Enter
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/yDMYKxy.png">
<br />
<br />
<br />
<br />



 - Right-click your active network adapter. Select "Properties"
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/6uH2zZJ.png">
<br />
<br />
<br />
<br />


 - Select "Internet Protocol Version 4 (TCP/IPv4)" and click "Properties"
 - Change "Default gateway" to pfSense VM's IP address (e.g., 192.168.1.185)
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/2XTTozG.png">
<br />
<br />
<br />
<br />


 -  Run `ipconfig /all` one more time to check if the default gateway is configured correctly.
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/YAynYah.png">
<br />
<br />
<br />
<br />
 
We should see the IP address of the pfSense VM. Now, our host network traffic goes via pfSense to the router and the internet!

---
[back to top](#toc)
## Testing the rules

<br />
<br />

 - Test the configuration:
    - Browse to various websites to ensure general internet access
    - Attempt to access the blocked website - it should not load
    - This confirms your pfSense firewall is working as intended!
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/8Md7kg5.png">
<br />
<br />
<br />
<br />






\<end\>

[back to top](#toc)

<br />
<br />
<br />

