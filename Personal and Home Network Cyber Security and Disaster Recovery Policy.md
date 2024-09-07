Date Created: 2024-09-04
Last Updated: 2024-09-05

## Policy Brief & Purpose

This personal security policy outlines the tools and methodologies that will be used to secure my personal and private digital assets. 

This policy will mitigate risk and loss by defining procedures for storing, handling, and transferring digital assets as well as procedures for mitigating loss during incidents as well as a disaster recovery plan.

## Scope

This policy applies to myself and all devices that I have legal ownership over. This policy is shared with and encouraged to be used by those who share residence with myself, friends, family, or otherwise to further reduce risk of data and asset loss. 

## Policy elements

#### Confidential Data

This data is secret and valuable. This policy outlines how to incorporate the cyber security triad to maintain the **Confidentiality, Integrity, and Accessibility** of our data. Relevant examples:

- Tax records
- Personal Journal/Diary
- Passwords
- Banking Information


#### Protect Personal Devices

Devices are the medium by which members of the home network access and interact with a variety of digital assets, either personal or public. Ensuring that all devices on the network are secure mitigates threats and risk to the data that is accessible on the network. To this end, all devices should:

- Be password protected.

- Have privileges defined on the networking level based on inherit risk of the device itself.

- Install security updates monthly or as soon as updates are available.


While it is not mandatory for all personal devices on the network, there are extra measures that I will take with devices under my personal control, to include:

- Full disk encryption 
  
- Webcam shutters
  
- Secure and auditable Operating Systems/Software



#### Emails

Emails remain one of, if not the most, common mediums of attacks for malicious actors. Here we outline some foundational protocols for handling emails as well as some higher level tools we can leverage for additional protection.

- Don't open attachments from unknown senders. 

- Be suspicious of clickbait titles and subject lines.

- Look for inconsistencies or "tells" of a malicious/spam email. (grammar mistakes, asking for information)

	**Additional Tools:**
		Because emails are a large medium of attack and because we must use email in some capacity to interact with our confidential data, (work, banking, taxes, etc) I have determined that the monetary value of the assets being protected warrants a budget to further secure it. To this end, the following additional tools are used:

	- A paid Proton Mail account which gets us access to:
		- Aliases 
		- Threat monitoring 
		- More advanced spam filtering
		
	- Yubikey 2FA authentication devices to secure the email account, and other accounts, which grants a higher level of security than SMS 2FA, which is susceptible to SIM Swap attacks. 



#### Manage Passwords Properly

Passwords are the keys to the kingdom and the assets within it. As such, securing them should be a top priority. Again, we are faced with a version of the Security Triad or CIA (Confidentiality, Integrity, Accessibility). Passwords must be kept a secret, they must also be hard to guess or brute-force, and they must be easily accessible so we can use our sensitive data to conduct our day-to-day tasks. The following protocols attempt to prioritize the confidentiality and security of the passwords, while still maintaining an acceptable level of accessibility. 

- Choose passwords with at least 12-22 characters (including capital and lower-case letters, numbers and symbols) 

- Avoid information that can be easily guessed in the password. (favorite color, dates, etc)

- Keep a different password for every account.

- Store passwords in KeepassXC database; A trusted, offline, auditable password manager. 

- NEVER use proprietary, custodial, or online password managers in a browser, plugin, or otherwise. 

- Change passwords every 6-12 months and after news of any breaches.



#### Transferring Data Securely

Transferring data introduces security risk. Some practices to help mitigate potential risks include:

- Use data transfer methods that align with the sensitivity of the data:
	- Networked home storage for users, and services that serve music, memes, and non-sensitive documents.
	- Flashdrives for semi-sensitive data.
	- Offline devices and audited media for highly sensitive data. 

- Avoid transferring extremely sensitive data from device to device unless necessary. Extremely sensitive data should only be transferred or reviewed on air-gapped devices. 

- Share confidential data over the home network or within home perimeter and not over public WiFi, unless using a VPN. (Tunnel back to home network preferred)

- Ensure that the recipients of the data are trusted and adhere to security policies.



#### Additional Operational Controls

Additional measures encouraged to use in the home to reduce risk of compromise:

- Secure and lock devices when not in use. 

- Duress PIN added to mobile devices that completely wipes them when entered. 

- Work with untrusted or not fully vetted software in a secure sandbox.
  
- Practice safe browsing habits like visiting only trusted sites and downloading files from trusted sources.
  
- Maintain a lean digital existence. (use as few devices as possible and have as few accounts as possible)



#### Additional Technical Controls

As the technical advocate of the home network, I will be tasked and responsible for:

- Installing and configuring firewalls, anti-malware software, authentication systems, etc.
  
- Arranging for security training and recommendations for all household members.
  
- Investigating security tools, incidents, breaches, etc. 
  
- Follow all policies and procedures in this document and lead by example.

Some additional Technical Controls that will be implemented as part of the home network infrastructure to help detect and reduce risk are:

- SIEM/IDS - A Wazuh server which all capable devices will report to. Allows us to detect threats sooner and patch vulnerabilities as they arise. 
  
- Network segmentation for devices with legacy connectivity protocols
	- Smart TV's, mobile devices, gaming consoles, etc on their own, individual networks. 
	- Guest network for guests and untrusted devices. 
	  
- A DNS filtering server (Pihole) that all devices will filter DNS requests through, reducing exposure to ads, which can be malicious. 
  
- New MAC address's blocked by default on the network unless approved manually by admin

- Only the latest and most secure Internet/WiFi protocols for primary devices. 



#### Incident Response, Recovery, and Research

Should a compromise or incident occur, the following steps should be followed. 

- Quickly identify the threat and all effected machines. 
- Identify the pros and cons of immediately bringing those machines offline. 
	- Pros: Immediately stop something like exfiltration or encryption
	- Cons: May leave us in the dark as to who attacked us and by which vector they were able to do so
- Contain and quarantine all effected machines so that they are not connected to the network or any important resources. 
- Run an autopsy on the machines and all effected files to learn more about what happened so it can be prevented in the future
	- checks logs
	- check file-system
	- retrace your own activities (was this a breach or was this invited in by negligence)
 - Patch and test the vulnerability
 - 



#### Backup, Redundancy, Protection Protocols

To ensure data is not lost due to compromise, error, or otherwise, a backup protocol will be implemented proportional to the value of the data being backed up. 

- Non-essential files can be stored on devices or user file shares on the home NAS. (to mitigate loss due to device failure, loss, breakage, etc)
  
- More important files will be stored on devices or user account shares on the home NAS and be included in a routine backup to warm storage. From the device they will be synced to the user share and from there be backed up to a large storage device attached to the NAS. 
  
- A routine backup of the home NAS to another warm storage device will take place every Sunday evening, to include all essential files. 
  
- From here, all data higher up in the sensitivity hierarchy will be separated into two groups:
  
	- Confidential files that under no circumstances can be seen by other eyes (example: bitcoin seed phrase, KeepassXC database) will be kept on an offline encrypted drive. Drive will be encrypted using Veracrypt and a SHA256(twofish(serpent())) scheme secured by a 24+ character password that will never be written down or recorded anywhere and will be memorized. 
	  
	- Sensitive data that needs an off-site back up will be kept in Proton Drive which is "trusted" to be encrypted and private. This is a situation where trust is sort of unavoidable, for my situation at least. So I trust Proton Drive more than another cloud provider because Proton Drive is secured by my Yubikey. This makes it more secure, if only marginally, than other options like safety deposit box, cloud storage or VM that dont have 2FA keys, or leaving the files with a relative. 

- Another cold backup of the warm backup is made and kept with relatives, just as a convenience recovery. This would be movies, music, very insensitive files, family photos, etc. 

- KeepassXC password database is kept on an encrypted drive (basically nested encryption) on my keychain.

- One Yubikey will be kept on person at all times and another as a backup in a secure, undisclosed location. 
  
	##### **Additional Backup and Protection Measures:**
	- NAS will use drives in RAID5 for added redundancy in case of drive failure or damage. 
	
	- Main infrastructure devices (NAS, Router, Servers) will be plugged into a UPS/Surge Protector combo to avoid electrical damage. 



### Disaster Recovery

Disaster Recovery depends heavily on the robustness and adherence to the backup protocols. 

One additional measure not mentioned as backup, because it technically is not, is having a live bootable USB, with a vetted and trusted image, on the keychain at all times, in addition to the KeepassXC backup and Yubikey. This combination means that from anywhere in the world, I should be able to use any host to securely access my data in the event of catastrophe. 

In the event that there is any kind of loss or compromise, given the technologies and protocols in place, we should be able to recover or at least continue to function in day-to-day tasks/work within 24 hours. Example situations and procedures outlined:

**Minimal data loss - Accidental loss, human error. Deleting files, breaking something, etc:**
- Try to fetch from trash bin or get into the device using live media to go grab the files. 
- If unsuccessful, grab the files from the warm backup if applicable. 

**Partial or 50% of data lost - Ransomware, exfiltration, power surge:**
- Respond to incident accordingly before attempting to bring data from backups forward.
- Recover from warm and local cold storage where possible. This should be possible in just about every non-catastrophic circumstance. 

**Total loss - House burned down, have to leave the country, doomsday:**
- All essential files, within a 7 day creation period, be available entirely remotely thanks to keeping a KeepassXC database and yubikey on person at all times. 
- I should have my keys on me if I am not at home, and if I am at home and need to leave my home, I just need to only grab my keys (and the cat) and I will be able to access all of my most sensitive information from any computer in a safe, secure, and private manner. 



#### Accepted Risks & Trade-Offs:

##### Keychain Recovery

The "keychain" recovery scheme is a great way to protect against total loss. It carries with it the risk of losing the keychain and having a stranger find it. A few things to consider and action should that occur:

- The drive that will contain the KeepassXC database will be encrypted with SHA(twofish(serpent)) making it extremely costly and time consuming to crack. Realistically, you should have plenty of time to recognize that you have lost your keys and to go in and set new passwords for all of your accounts before a stranger or even a knowledgeable attacker is able to compromise your database. That being said, there are hardware hacks that an advanced attacker could potentially employ that may allow them to circumvent the encryption all together. I think the likelihood of such a sophisticated attacker finding your keys is less than your house burning down, though it's hard to really quantify I suppose. 
  
- The Yubikey on the other hand will be able to be plugged into any device and, so long as the Yubikey software is installed on that software, they will be able to see your One Time Password and the name of the account they are associated with. However there will not be any personally identifiable information on the Yubikey that clue a bad actor on whose account they belonged to. It is important to keep it this way and ensure that there is absolutely no way to associate the keys, and anything on the keys, with your identity. This includes making sure that your name or PII is no where on your live USB. 

##### KeepassXC

KeepassXC does have some known vulnerabilities. However these vulnerabilities require direct physical access to the machine in order to be exploited. I believe this level of risk is acceptable and preferable in comparison to the alternative available. 


## Closing

These policies and procedures should help reduce risk where possible and provide a robust security posture that should protect adherents from a plethora of attacks and circumstances that would otherwise result in loss of valuable assets. This policy is a living document that will continue to evolve as the threat landscape and needs of the user evolve. 