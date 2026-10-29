# Wazuh-SIEM-project
SIEM lab using Wazuh for security monitoring
A small lab that deploys an open-source Wazuh SIEM and uses File Integrity Monitoring (FIM) to detect file changes on a Windows endpoint in real time.
1. Business Scenario

A small organisation has no budget for a commercial SIEM but needs to know when sensitive files on employee workstations are created, modified or deleted, whether through insider misuse, malware or misconfiguration. This lab shows that Wazuh can provide centralised log collection, real-time FIM alerting and a searchable dashboard at no licence cost.

2. Architecture
<img width="1095" height="693" alt="image" src="https://github.com/user-attachments/assets/5ba05c4d-4a46-470d-863f-98dfa6117a1c" />


3. Methodology
Prepare: VirtualBox, Ubuntu VM with internet access, admin rights on Windows.
Install the manager (Ubuntu): add the Wazuh GPG key, then run the all-in-one installer
   curl -sO https://packages.wazuh.com/4.16/wazuh-install.sh && sudo bash ./wazuh-install.sh -a -i
Open the dashboard at https://<ubuntu-vm-ip>. Accept the self-signed certificate warning and log in with the credentials printed at the end of installation.
Install the agent on Windows using the official MSI with default settings.
Register the agent: on Ubuntu run sudo /var/ossec/bin/manage_agents, add an agent (A) and extract its key (E). On Windows, paste the key into Wazuh Agent Manager, enter the manager's IP and restart the agent service.
Enable FIM: edit C:\Program Files (x86)\ossec-agent\ossec.conf and add:
   <directories realtime="yes">C:\Users\abc\Test</directories>

   4. Mitigation

FIM is a detective control: it tells you a change happened but does not stop it. Pair it with:

Least privilege and NTFS permissions on sensitive folders.
Alert triage: review FIM alerts and investigate unexpected changes.
Active Response (optional): Wazuh can trigger automated actions on specific alerts.
Backups to recover tampered or deleted files.
Lab hardening: replace default credentials, restrict dashboard access to trusted IPs and keep Wazuh up to date.

5. Findings Mapping

The guide covers setup and verification only. The table below maps the expected FIM events to Wazuh rules and MITRE ATT&CK for context. Confirm rule IDs and technique tags against your own alerts.
<img width="1951" height="860" alt="image" src="https://github.com/user-attachments/assets/4b60f0db-be9c-49a2-a93a-737775fa0e49" />

6. Tools & References

Tools: Wazuh (Manager, Indexer, Dashboard, Agent, Syscheck), Ubuntu Server 26.04.1, VirtualBox, Windows host.

References:

-Original guide and lab by Royden Rebello (The Social Dork)

-Wazuh documentation: https://documentation.wazuh.com

-MITRE ATT&CK: https://attack.mitre.org
