# Wazuh-SIEM-project
SIEM lab using Wazuh for security monitoring
A small lab that deploys an open-source Wazuh SIEM and uses File Integrity Monitoring (FIM) to detect file changes on a Windows endpoint in real time.
1. Business Scenario

A small organisation has no budget for a commercial SIEM but needs to know when sensitive files on employee workstations are created, modified or deleted, whether through insider misuse, malware or misconfiguration. This lab shows that Wazuh can provide centralised log collection, real-time FIM alerting and a searchable dashboard at no licence cost.
2. Architecture
Component	Host	Role
Wazuh Manager + Indexer + Dashboard	Ubuntu Server 20.04+ (VirtualBox, bridged adapter)	Collects, analyses, stores and visualises agent data
Wazuh Agent	Windows host machine	Sends logs and file-change events to the manager
