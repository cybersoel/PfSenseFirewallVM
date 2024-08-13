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

- 

---

---

<h4>Tip: Any configuration options not mentioned in the walkthrough can be left at their default settings</h4>

---



---

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
## pfSense Web Application Configuration

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



19
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/UBoQt71.png">
<br />
<br />
<br />
<br />




20
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/N3aAMlm.png">
<br />
<br />
<br />
<br />


21
<p align="center">
<br/>
<img width="540" alt="Portfolio" src="https://i.imgur.com/DQjUHSQ.png">
<br />
<br />
<br />
<br />






22
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/K1tY1ui.png">
<br />
<br />
<br />
<br />






23
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/tt51UUx.png">
<br />
<br />
<br />
<br />






24
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/CE8SJXK.png">
<br />
<br />
<br />
<br />






25
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/NMNDPVo.png">
<br />
<br />
<br />
<br />






26
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/qKGuOxK.png">
<br />
<br />
<br />
<br />






27
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/egtFHS2.png[">
<br />
<br />
<br />
<br />






28
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/AvbnDYI.png">
<br />
<br />
<br />
<br />






29
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/yCmaXKl.png">
<br />
<br />
<br />
<br />






30
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/Np1u3IZ.png">
<br />
<br />
<br />
<br />






31
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/7ecaTCJ.png[">
<br />
<br />
<br />
<br />






32
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/1asDdqO.png">
<br />
<br />
<br />
<br />






33
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/Te89Q9P.png">
<br />
<br />
<br />
<br />






34
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/xeAsa71.png">
<br />
<br />
<br />
<br />






35
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/oQxNm90.png">
<br />
<br />
<br />
<br />






36
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/znR1Eue.png">
<br />
<br />
<br />
<br />






37
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/Cb44JLX.png">
<br />
<br />
<br />
<br />






38
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/OS3qxNR.png">
<br />
<br />
<br />
<br />






39
<p align="center">
<br/>
<img width="680" alt="Portfolio" src="https://i.imgur.com/qzyLdb6.png">
<br />
<br />
<br />
<br />






40
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/KEKaJGz.png">
<br />
<br />
<br />
<br />






41
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/TMJsTNr.png">
<br />
<br />
<br />
<br />






42
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/yDMYKxy.png">
<br />
<br />
<br />
<br />






43
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/6uH2zZJ.png">
<br />
<br />
<br />
<br />






44
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/2XTTozG.png">
<br />
<br />
<br />
<br />






45
<p align="center">
<br/>
<img width="597" alt="Portfolio" src="https://i.imgur.com/YAynYah.png">
<br />
<br />
<br />
<br />






46
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

