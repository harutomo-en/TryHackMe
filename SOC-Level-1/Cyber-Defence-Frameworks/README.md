# **Cyber Defense Frameworks**
> *TryHackMe SOC Level 1 Module*

**Table of Contents**
- [Junior Security Analyst Intro](#junior-security-analyst-intro)
- [Pyramid of Pain](#pyramid-of-pain)
- [Cyber Kill Chain](#cyber-kill-chain)
- [Unified Kill Chain](#unified-kill-chain)
- [Diamond Model](#diamond-model)

A collection of noted and a summary of what I have learned from TryHackMe's SOC Level 1's Cyber Defence Framework module.

## Junior Security Analyst Intro
---
*What does a Junior Securty Analyst do?*: A Junior Security Analyst is supposed to be a _Triage Specalist_ and a primary part of their job is meant monitoring log data and managing IDS and IPS alerts as well as managing other security tools.

Junior Security Analysts are only meant to configure and implement security solutions and tool configuration and if a security incident occurs, it should be reported and escalated to a highter tier team in the Security Operations Center.

#### **What is a SOC?**
---
A Security Operations Center (SOC) is a team that handles the prevention, monitoring, investigation, and the response to cyber security threats.  A SOC is a 24 hour operation that is always active.

This image displays the responsibilities included for the SOC:
###### Source: TryHackMe
<div align="center">
<img src="https://i.imgur.com/s39NuzG.png" align="center" width="600"></img>
</div>

To elaborate on this circle of responsiblities, the best place to start is with _Log Collection_

**Log Collection** is the collection and maintainence of log files that store all the activity and communications taking place on the networks relevent to the SOC.  Logging these activities allows for tracing back and pinpointing any past actions that have affecting a security incident.  Log collection and analysis is also important for establishing a baseline for normal activity, increasing the effectiveness of IDS and IPS systems. 

**Knowledge Base** refers to an understanding of existing security standards, vulnerabilities, attack vectors, and available tools necessary for ensuring the confidentiality, integrity, and availability of an organization's services, networks, and data.  

**Research and Development** refers to the continious education necessary in the field of cybersecurity.  Day by day, new vulnerabilities are discovered, new patches are developed and released, and new security tools are made available to improve security operations.  To maintain security, keeping up to date with these changes and developing solutions to newfound problems is essential.

**Aggregation and Correlation** refers to organizing and standardizing a large amount of data, usually log data, and analyzing them to provide meaningful information for security analysts.

**Threat Intelligence** refers to gaining information about possible threats to an organization's security, such as new phishing techniques or the attack vectors of new popular malware.

**SIEM**, or a Security Information and Events Manager, is a type of software that combines the capabilities of a Security Information Manager (SIM) with a Security Event Manager (SEM).  A SIEM's primary capabilty is it's a bility to aggregate and analyze data from an organization's security framework and provide an analysis on a single dashboard.  The SIEM supports a Security Operation Center's incident response capabilities.

**Reporting** is how a SOC communicates their findings to the management of an organization.  This both enables transparency to management regarding the security of their company, as well as allowing management to dictate what type of response to major incidents should be implemented.

A nice website I found on SOC reports is available [here]("https://www.bitsight.com/blog/a-security-operations-center-report-template").

**Ticketing** refers to the case management and assignment method used in Security Operation Centers.  When a potential incident occurs, the case should be assigned and tracked until the case's closure to ensure that it was properly handled.  This is the function of ticketing.


## Pyramid Of Pain
---

## Cyber Kill Chain
---

## Unified Kill Chain
---

## Diamond Model
---