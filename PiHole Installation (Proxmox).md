Date Created: 2024-08-31
Last Updated: 2024-09-02

#### Goal: 
Spin up a virtual machine for PiHole so that we can filter and block DNS requests on our home network

#### Equipment needed: 
- A home internet connection
- A working computer that can download the necessary files for this project
- A destination host with sufficient specifications to install the PiHole package. Can be a dedicated server machine or Virtual Machine (in this instance I will be installing on a Virtual Machine on my Proxmox Server).


## Phase 1: Set up the Virtual Machine for Pihole

1. Using my personal device, I downloaded a Ubuntu LTS ISO image off of the official [Canonical](https://ubuntu.com/download/server) website. 

2. I verified the checksum of the file that I downloaded with the one that they provide on their website using "EasyHash". The Checksum matched so I continued.
   
3. In Proxmox, I added the ISO to my "Local Storage" > "ISO Images" section of my datacenter. 
   
4. Now, I click on "Create VM" in the top right-hand of the interface and begin inputting the settings for my PiHole server:
	- **General**: left everything default and named the VM "pihole"
	- **OS**: Selected my Ubuntu ISO image and left everything else default
	- **System**: I left everything here default
	- **Disks**: I gave the VM a diskspace of 8gb. 4gb probably would be fine but I like having some headroom for future updates and log storage. Also enabled "Discard" which trims blocks that have been marked as unused. 
	- **CPU**: I did 1 Socket and 4 cores. 2 cores is probably plenty, but I have more than just me in the house and new devices are added all the time, so I like have the headroom.
	- **Memory**: I did 2gb which will be plenty. Under load it tops out at like 1gb. 
	- **Network**: I kept all of the defaults. 
	- **Confirm**: confirmed all of the settings and launched the VM

## Phase 2: Install Pihole

1. Following the One-Step automated install from the official PiHole site
		`curl -sSL https://install.pi-hole.net | bash`

2. I was walked through a series of prompts:
	1. I chose Cloudflare as the upstream DNS provider
	2. PiHole installation will then prompt for which ad-lists to use for blocking. I selected all of them. 
	3. Installation then asks if I wish to keep the current IP address as the static address. I chose yes. 
	4. In the next step, I kept the admin portal addition checked. 
	5. I left "log queries" turned on and used Level 1 privacy settings. 
	6. I confirmed all of the changes and wrote down the Admin password provided at the end of the installation.
3. Success!

## Phase 3: Logging in to PiHole and further configuration

1. I navigated to the admin portal for the PiHole in my web browser and put in the Admin password. 
2. I navigated to the "Settings" tab and went through all of child tabs and made changes where needed
	1. System - No changes here.
	2. DNS
		1. I checked **"Never forward non-FQDN `A` and `AAAA` queries"**
		2. I checked "**Never forward reverse lookups for private IP ranges**"
	3. DHCP - No changes here. I won't be using PiHole as a DHCP server at the moment, but plan to in the future. 
	4. Web Interface - Picked my favorite dark-mode theme B)
	5. API - No changes here.
	6. Privacy - No changes here (should be the same as what was chosen during installation)
	7. Teleporter - No changes here.
3. All done!

## Phase 4: Router Configuration

1. In order to get your DNS requests to go through PiHole, your router must be configured so that it uses your PiHole for DNS queries instead of going straight to whatever it would normally use. This step may be slightly different for everyone depending on their router and firmware, but it should be under the same general location. I went to my routers DNS settings and put in my PiHole servers IP address in place of the IP that was already there. So for example, if the router is using Googles DNS (8.8.8.8) and I want to use my PiHole (192.168.1.5) I would replace the 8.8.8.8 address with 192.168.1.5. 
2. In many cases, your router will have a backup DNS server. If you have 1 Pihole, you can keep your preferred default DNS server as the backup. In my case, I built a separate physical PiHole on a Raspberry Pi and used its address as the backup. This means that if anything happens to either one of them, I will have a redundant backup. And because they are not both physical or both on Proxmox, the likelihood that they are both down at the same time is reduced. 
3. I reboot the router and reboot all of my devices and their DNS requests are now being filtered! I can confirm this by looking at the PiHole admin dashboard and seeing the client list which is now populated with all of my devices. 

## Success!

