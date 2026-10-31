# Eviction

<img width="1355" height="306" alt="image" src="https://github.com/user-attachments/assets/ab75f477-cc5a-43b9-ac93-f09fcd904705" />

Sunny is a SOC analyst at E-corp, which manufactures rare earth metals for government and non-government clients. She receives a classified intelligence report that informs her that an APT group (APT2...) is targeting the company’s strategic operations. The report suggests a coordinated intrusion attempt against E-corp’s systems and emphasizes the potential theft of sensitive data related to rare earth procurement, research, and government-facing contracts.

The threat scenario indicates that the attacker is likely using a multi-stage intrusion strategy to gain access, establish persistence, steal credentials, move laterally, and exfiltrate sensitive material. As a SOC analyst, Sunny’s job is to confirm the intrusion, identify the initial access method, determine the scope of compromise, and document the attack for containment and response.

## Initial Assessment

The first step in any SOC investigation is to establish whether the suspicious activity is isolated or part of a broader intrusion. In this case, the indicators point to a sophisticated adversary using common attack tradecraft rather than opportunistic malware.

A typical APT intrusion flow would include:

- Initial access through phishing, malicious documents, or a compromised external vector
- Execution of script or payload on a user endpoint
- Privilege escalation or credential harvesting
- Lateral movement within the internal network
- Persistence to maintain access over time
- Collection and exfiltration of sensitive files

The screenshots included in the room show a sequence of investigations into suspicious endpoints, process execution, persistence mechanisms, and likely credential abuse. This indicates the compromised host was not simply infected with a single malicious binary; rather, it appears to be part of a larger intrusion chain.

## Investigating the Host

The investigation begins with one or more endpoints showing suspicious activity. In a real SOC workflow, the analyst would review:

- Process creation history
- Parent-child process relationships
- User logons and source IPs
- Scheduled tasks and services
- Registry modifications
- File writes in temporary folders
- Network connections to external domains or IPs

From the evidence presented in the challenge, the endpoint likely showed execution of a malicious script or payload. Attackers frequently use legitimate Windows tools such as:

- PowerShell
- WMI
- rundll32.exe
- regsvr32.exe
- mshta.exe
- cmd.exe
- wscript.exe

These tools allow attackers to disguise malicious behavior within normal administrative tasks.

## Persistence and Defense Evasion

One of the strongest indicators of compromise is evidence of persistence. Attackers often add scheduled tasks or registry keys so that their malware executes automatically after reboot or user logon.

Likely persistence methods in this scenario include:

- Registry Run keys
- Startup folder entries
- Scheduled tasks
- Windows services
- WMI event persistence

This is important because it distinguishes a single malicious execution from an active foothold. If the malicious script or binary is still running after reboot or login, the attacker has successfully maintained access.

Additionally, defensive evasion is likely present. The adversary may be:

- Using encoded PowerShell commands
- Running scripts from temporary directories
- Hiding tasks or file names to avoid analyst scrutiny
- Executing payloads from user-writable locations such as AppData or temp

These techniques are common in APT intrusions and are often seen during initial investigation.

## Credential Access and Lateral Movement

Once execution succeeds, the attacker’s next objective is usually privilege abuse or credential theft. The screenshots strongly suggest activity consistent with credential harvesting.

This can include:

- Dumping LSASS memory
- Extracting credentials from browser or local security stores
- Passing credentials over the network
- Using stolen Kerberos tickets or NTLM hashes
- Leveraging remote admin tools to pivot to other systems

Successful credential access would explain the subsequent internal movement. Attackers often move quickly after a host is compromised, especially when they obtain administrative credentials.

The room likely demonstrates lateral movement through:

- SMB file sharing
- Remote Service creation
- PsExec or similar tools
- RDP or WinRM usage
- Remote scheduled tasks
- WMI or remote command execution

At this stage, the SOC should be concerned about active compromise of additional endpoints and possible domain-level access.

## Data Staging and Exfiltration

The final phase of the intrusion chain is data collection and theft. E-corp’s business model makes it a high-value target because the company deals in rare earth metals and sensitive government-related information. This makes exfiltration especially dangerous.

Attackers would likely search for and collect:

- Procurement data
- Technical research documents
- Internal financial records
- Contracts or government-facing reports
- Sensitive operational plans
- Design or engineering files

The evidence from the challenge likely shows files being accessed, compressed, renamed, or copied into staging areas before being sent outside the network. Staging behavior is often visible through:

- ZIP/RAR creation
- Copies to hidden folders
- Use of PowerShell to archive or export files
- Unexpected outbound traffic to external IPs or cloud services

This indicates the attacker was not just exploring the system—they were preparing to steal and possibly monetize or weaponize the data.

## SOC Response and Mitigation

Once compromise is confirmed, the response must be fast and precise. The following response actions are essential:

1. Isolate affected hosts from the network
2. Block malicious domains and IPs from external communication
3. Reset credentials for impacted accounts, especially privileged users
4. Remove persistence mechanisms and malicious auto-start entries
5. Hunt for related compromise across internal systems
6. Review logs for lateral movement and suspicious remote administration
7. Preserve forensic evidence before remediation
8. Rebuild compromised systems if necessary

The goal is not only to remove the threat but also to answer the critical incident questions:

- How did the attacker get in?
- What systems were compromised?
- What was the attacker trying to steal?
- Did the attacker move beyond the initial host?
- What is the overall scope of the intrusion?

## Key Takeaways

This challenge highlights several important SOC analyst concepts:

- Not all suspicious activity is malware; every event must be placed in context
- Process lineage and persistence are critical to understanding attack progression
- Credential access is often the pivot point between initial compromise and broad network impact
- Lateral movement is a strong indicator of a serious intrusion
- Data staging and exfiltration are often the true objective of APT activity

In short, the Eviction scenario is a realistic example of how a sophisticated attacker tries to gain a foothold, maintain access, escalate privileges, and steal strategic data. The SOC analyst’s job is to correlate the evidence across the environment and produce a clear, defensible narrative of the attack.

## Final Conclusion

Sunny’s investigation confirms the importance of thorough alert validation, endpoint forensic analysis, and cross-system correlation. The attack does not appear to be a simple malware infection; it is consistent with a professional intrusion campaign designed to steal sensitive information from an organization operating in a high-value sector.

The evidence supports the conclusion that an APT-style intrusion was underway, involving suspicious execution, persistence, credential abuse, lateral movement, and likely theft of sensitive corporate and government-related data. The final response should include immediate containment, a full threat hunt, and recovery actions to prevent further compromise.

<img width="1351" height="598" alt="image" src="https://github.com/user-attachments/assets/12cb1852-c1b7-4cf9-ad59-54b57e4b5a78" />
<img width="1351" height="597" alt="image" src="https://github.com/user-attachments/assets/3ece0766-ac45-4250-bd1d-2c489ea81a22" />
<img width="1350" height="598" alt="image" src="https://github.com/user-attachments/assets/132c2371-a396-45d3-a64c-583b52612dad" />
<img width="1349" height="596" alt="image" src="https://github.com/user-attachments/assets/fa5e4d6f-b5f0-40ec-bf7e-907ca19c0e88" />
<img width="1237" height="543" alt="image" src="https://github.com/user-attachments/assets/8d72707a-f7e5-4a20-8b85-0ae94a221624" />
<img width="1254" height="530" alt="image" src="https://github.com/user-attachments/assets/58738593-c732-40c8-852b-d9273c99ff9d" />
