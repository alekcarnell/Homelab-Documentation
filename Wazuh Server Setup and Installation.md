Date Created: 2024-07-15
Last Updated: 2024-08-30

#### Goal: 
Build a home network SIEM/IDS server that will monitor the logs of our home devices and let us know if there are any vulnerabilities or events that should concern us. 

#### Equipment needed: 
- A home internet connection
- A working computer that can download the necessary files for this project
- A destination host with sufficient specifications to install the [Wazuh](https://wazuh.com/) software. Can be a dedicated server machine or VM (in this instance I will be installing on a Intel NUC).


## Phase 1: Setting up the server hardware

1. I chose a Intel NUC that I had lying around. It has 8gb of RAM, a 1TB SSD, and a sufficient processor. 

2. I booted into the BIOS and changed some of the configuration:
	- Turned off secure boot (temporarily) so I could boot from a USB drive with Ubuntu on it. 
	- Set a secure BIOS password

3. Using my personal device, I downloaded a Ubuntu LTS ISO image off of the official [Canonical](https://ubuntu.com/download/server) website. 

4. I verified the checksum of the file that I downloaded with the one that they provide on their website using "EasyHash". The Checksum matched so I continued.

5. I copied the ISO directly to a flashdrive that has been configured with [Ventoy](https://www.ventoy.net/en/index.html). Without Ventoy, the user will need to write the ISO onto the flashdrive using something like [Rufus](https://rufus.ie/en/) or [Balena Etcher](https://etcher.balena.io/). 

6. I plugged the flashdrive into the NUC, powered on the device, and pressed F10 to go to the boot menu.

7. After selecting the flashdrive I was taken to the Ventoy menu, where I scrolled and selected the Ubuntu 22.0.4 image I had just downloaded and verified. 

8. Upon booting, I went through the Ubuntu installer, step by step. I won't list every step but I chose defaults for just about everything. 

9. After installation, I reboot the device, turned Secure Boot back on, logged in, and did some very quick checks to look for anything out of place. The checksum matched so it "should" be alright, but in case a false checksum was hacked into the website, I still checked the OS for irregular processes, files, directories, etc. I did not use a tool for this, but absolutely would in a deployment that I plan to keep. Everything looked alright. 

10. Before unplugging the monitor and keyboard/mouse, I made sure to install and enable SSH services on the server with:

	`sudo apt install openssh-server`

11. After network connectivity had been established, I continued the rest of the configuration via SSH from my main PC

12. I made sure the system was up to date with:

	`sudo apt-get upgrade && apt-get update`

13. I am now ready to install Wazuh


## Phase 2: Installing the Wazuh server software

1. Still SSH'd into the newly configured server, I download and install the Wazuh package based on the instructions from https://documentation.wazuh.com/current/quickstart.html. Wazuh consists of 3 components and this should give you all 3. 

2. The installation was very straightforward, like installing any other package really. After it was complete, I navigated to the server IP to view the Web-based interface. 

3. I proceeded to install the agents on my endpoints, starting with a spare laptop that I use (windows). The endpoint software installs with an executable that prompts you for the "manager IP" and an "authentication key". The manager IP is the Wazuh server IP and I left the authentication key blank.   

> [!NOTE]
> I did mess this up at first by putting the incorrect IP address in. I put the IP of my endpoint by accident when it should have been the IP of the Wazuh server. To fix this, I uninstalled and purged the package and reinstalled using the script that they provide, this time with the correct IP and it worked flawlessly. 

6. Upon refreshing the web-based interface dashboard, I now saw my endpoint registered and successfully forwarding it's logs (windows logs) to the server for analysis. 

7. Success!
