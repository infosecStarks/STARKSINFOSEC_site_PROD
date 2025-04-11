---
id: 273
title: 'Into the Eye of the Storm: An In-depth Look at APT Group Volt Typhoon'
date: '2023-06-30T11:23:12+10:00'
author: Byte
layout: post
Type: post
guid: 'https://starksinfosec.com/?p=273'
permalink: /Into-The-Eye-Of-The-Storm/
image: '/images/volt-typhoon.webp'
categories:
    - News
    - Research
tags:
    - blog
    - infosec
    - research
    - security
---

## **Introduction**

Have you ever wondered about the intricate world of cyber espionage and how state-sponsored actors operate in the shadows? Imagine an organised, elusive group with the resources of a nation behind them, tirelessly working to infiltrate some of the most protected systems in the world. This is not the premise of a spy novel but the reality of Advanced Persistent Threat (APT) groups, one known as Volt Typhoon.

In recent news, Volt Typhoon, a state-sponsored actor suspected to be based in China, has come under the spotlight due to its sophisticated attacks on critical infrastructure across multiple sectors in the United States, particularly in Guam. The group’s stealthy tactics, living-off-the-land techniques, and targeted approach have raised alarms in the cybersecurity community.

In this 2 part blog post, in part 1, we will dive into the world of Volt Typhoon, uncovering their tactics, techniques, and procedures (TTPs) and exploring the potential implications of their activities. In part 2 of our blog series, we will take you on a journey through a lab scenario that simulates their attack, providing a clearer understanding of their modus operandi and how to mitigate such threats. So, buckle up as we navigate the diverse landscape of Volt Typhoon’s cyber espionage operations.

## **Background of Volt Typhoon ⚡️🌀**

### **A Closer Look at Volt Typhoon – A Shadow in the Cyberspace**

Who is Volt Typhoon? They are a state-sponsored Advanced Persistent Threat (APT) backed by China 🇨🇳, currently known for espionage and gathering intelligence. They were first identified in mid-2021 by[Microsoft](https://www.microsoft.com/en-us/security/blog/2023/05/24/volt-typhoon-targets-us-critical-infrastructure-with-living-off-the-land-techniques/), targeting critical infrastructure in the U.S. and Guam, spanning various sectors like communications, manufacturing, information technology, and more. The threat actors’ behaviour suggests they intend to maintain access without being detected for as long as possible. But what makes them different to other APT groups?

Well, this is where things get interesting. The threat actors’ use of “living off the land” involves using built-in network administration tools like[wmic](https://attack.mitre.org/techniques/T1047/),[netsh](https://attack.mitre.org/software/S0108/),[PowerShell](https://attack.mitre.org/techniques/T1059/001/), and[ntdsutil](https://attack.mitre.org/techniques/T1003/003/). When using these tools, the threat actor blends in with regular Windows Activities and network traffic, which makes it more difficult to detect and allows them to stay under the radar, But I will get more into their tactics later on. And in part 2 of the blog, we will showcase what the tools do and go into detail about how effective they can be.

<figure class="wp-block-image">![](https://lh4.googleusercontent.com/sIPZeiDHmxl0CWob064mHzkvl2DikrMu7sW9dKSWN4HX4iuIsooyN-hz2ZgVWnNi4XaYPj2xm6A3B17673pgvGeD4D5vY2pkkpV3zzRIFYGsT4_So8gbB9r19U0QYTA0TezeyLiIb0IjT3YqntkPlRM)</figure><span class="fonts-plugin-block " style="font-family: verdana;font-weight: normal;font-size: 15px;color: #707376">*Figure 1. Volt Typhoons attack diagram( Source:*[ Microsoft*](https://www.microsoft.com/en-us/security/blog/wp-content/uploads/2023/05/Figure-1-storm-0391-attack-diagram.webp)*)*</span>What are Volt Typhoons’ reasons behind targeting U.S. and Guam critical infrastructure? And what intentions does China have for this type of Intelligence? Well, let us dive into that —&gt;

The reasons behind targeting Guam, in particular, is a crucial strategic location due to the presence of three critical U.S. military bases. By targeting Guam, Volt Typhoon potentially gains access to sensitive military information. With all this information and intelligence, some analysts have expressed concerns that the attacks by Volt Typhoon could be a precursor to larger, more destructive operations, potentially willing a sabotage element; recently, senators have been issued ‘Emergency’[satellite phones](https://www.cbsnews.com/news/senators-issued-satellite-phones-new-security-measures/) in case of telecommunication disruption. If you look at the bigger picture, you can see China has been accused of cyber espionage and gathering intelligence, not just with Volt Typhoon but with other APT Groups, which also show similar tactics to Volt Typhoon. More on Guam later on.

[APT 41](https://socradar.io/5-facts-you-should-know-about-apt41-double-dragon/) (been active since 2014) – Chinese hacking team, which has also been known as Wintti, Double Dragon and Amoeba. They have conducted a mix of government-backed cyber attacks and finically motivated data breaches, according to cybersecurity firms Mandiant and FireEye.[Reuters](https://www.reuters.com/technology/chinese-groups-accused-hacking-microsoft-us-others-2023-05-25/) Here says, “The U.S Secret Service said the team had stolen U.S. COVID relief benefits worth tens of millions of dollars between 2020-2022.”

Chinese authorities have returned and described such reports as “groundless accusations.”

More recently, China has been accused of hacking the Kenyan Government due to its growing debt to Beijing —&gt; ([https://www.reuters.com/world/africa/chinese-hackers-attacked-kenyan-government-debt-strains-grew-2023-05-24/](https://www.reuters.com/world/africa/chinese-hackers-attacked-kenyan-government-debt-strains-grew-2023-05-24/) ) Reuters explains that the assessed hacks are aimed at gaining information on debt being owed to Beijing by the East African nation. As President Xi Jinping’s plan for a global infrastructure network, Kenya is a strategic link in the Belt and Road Initiative. The Chinese foreign ministry said that “they are not aware” of any such hacking.

This wave of cyber intrusions signifies China’s preparedness to harness its spy capabilities to scrutinise and secure its international economic and strategic stakes.

## **Technical Analysis of Volt Typhoon’s Techniques**

In our previous discussion, we delved into the strategic motivations behind Volt Typhoon and the specific infrastructure they set their sights on. Now, let’s dive deeper into the fascinating realm of their operational techniques. How exactly do they execute their attacks? What tools do they employ, and what tactics do they employ? By unravelling these technical aspects, we can not only gain valuable insights into their operational methods but also equip ourselves with the knowledge to defend against their ever-evolving threats effectively. So, brace yourself for an immersive journey into the intricate world of cyber espionage.

The group initiates its activities by compromising specific small office/home office (SOHO) routers through the internet-facing Fortinet FortiGuard systems and appliances for initial access. Once inside, they exploit any available privileges and extract credentials associated with Active Directory accounts utilised by these devices. Public reports have identified a range of equipment that the group may utilise. This includes but is not limited to, devices from manufacturers such as ASUS, Cisco, D-Link, Netgear, and Zyxel.

The services and applications used in exploitation are:

- Fortinet Fortiguard devices
- Zoho ManageEngine ADSelfService Plus ([NVD – CVE-2021-40539 (nist.gov)](https://nvd.nist.gov/vuln/detail/CVE-2021-40539))
- Paessler PRTG monitoring software

Notably, specific tools, like ManageEngine, have been utilised by various other adversaries in the past, while detailed information about the use of other tools remains undisclosed at this time. The group’s primary focus lies in exploiting server-side or application-side vulnerabilities for initial intrusions into victim systems. Here is a simple diagram of their attack process.

<figure class="wp-block-image">![](https://lh3.googleusercontent.com/N6F98T4s-M_4KFb35D7aMMgxBYvbmcwePYDg21hVD3XuegsCITZFGuuac8G908pXFeffM-utG1w859PJ97bkjcsp9eYLviiL7CWooUl6MsjqGeLzgEaA1QGrl4T0nU0xNwoZHnjaiA_oyFNH2BYe6mw)</figure><span class="fonts-plugin-block " style="font-weight: normal;font-size: 18px;color: #707376">*Figure 2. Volt Typhoon Attack Process*</span>Volt Typhoon relies on open-source software such as Earthworm and a customised Fast Reverse Proxy (FRP) client to obscure their network traffic. They employ a hardcoded Command and Control (C2) callback to specific ports, namely 8080, 8443, 8043, 8000, and 10443, using a variety of filenames. Some examples of these filenames include cisco\_up\[dot\]exe, cl64\[dot\]exe, vm3dservice\[dot\]exe, watchdogd\[dot\]exe, Win\[dot\]exe, WmiPreSV\[dot\]exe, and WmiPrvSE\[dot\]exe. This enables them to conceal their activities and maintain a covert presence within the target. The source is here, where the NSA published a detailed[ PDF document](https://media.defense.gov/2023/May/24/2003229517/-1/-1/0/CSA_Living_off_the_Land.PDF) on the group. Ok, let’s go through each step in their techniques and explain it.

### **Initial Access**

## **T1078 Valid Accounts &amp; T1190: Exploiting Public-Facing Applications**

Volt Typhoon use of Valid accounts and exploits Public facing applications. In this scenario, we see Volt Typhoon compromise SOHO devices using this CVE – CVE-2021-40539 and CVE-2021-27860 RCE vulnerabilities for initial access once a device has been compromised. They extract any valid AD credentials to compromise any critical infrastructure. List of other CVEs listed below possibly used during their attacks.

<figure class="wp-block-table">| *Incident ID* | *NVD CVE* | *Product* | *Severity* | *Description* |
|---|---|---|---|---|
| [*FG-IR-23-097*](https://www.fortiguard.com/psirt/FG-IR-23-097) | [*CVE-2023-27997*](https://nvd.nist.gov/vuln/detail/CVE-2023-27997) | *FortiOS* | *9.2 (Critical)* | *Heap buffer overflow in SSL-VPN pre-authentication* |
| [*FG-IR-23-111*](https://www.fortiguard.com/psirt/FG-IR-23-111) | [*CVE-2023-29180*](https://nvd.nist.gov/vuln/detail/CVE-2023-29180) | *FortiOS* | *7.3 (High)* | *Null pointer de-reference in SSLVPNd* |
| [*FG-IR-22-475*](https://www.fortiguard.com/psirt/FG-IR-22-475) | [*CVE-2023-22640*](https://nvd.nist.gov/vuln/detail/CVE-2023-22640) | *FortiOS* | *7.1 (High)* | *FortiOS – Out-of-bound-write in SSLVPNd* |
| [*FG-IR-23-119*](https://www.fortiguard.com/psirt/FG-IR-23-119) | [*CVE-2023-29181*](https://nvd.nist.gov/vuln/detail/CVE-2023-29181) | *FortiOS* | *8.3 (High)* | *Format String Bug in Fclicense daemon* |
| [*FG-IR-23-125*](https://www.fortiguard.com/psirt/FG-IR-23-125) | [*CVE-2023-29179*](https://nvd.nist.gov/vuln/detail/CVE-2023-29179) | *FortiOS* | *6.4 (Medium)* | *Format String Bug in Fclicense daemon* |
| [*FG-IR-22-479*](https://www.fortiguard.com/psirt/FG-IR-22-479) | [*CVE-2023-22641*](https://nvd.nist.gov/vuln/detail/CVE-2023-22641) | *FortiOS* | *4.1 (Medium)* | *Format String Bug in Fclicense daemon* |

</figure>*CVE table –* *Source*[ Fortinet*](https://www.fortinet.com/blog/psirt-blogs/analysis-of-cve-2023-27997-and-clarifications-on-volt-typhoon-campaign)

### **Execution**

##### **T1047 Windows Management Instrumentation &amp; T1086 PowerShell**

During the execution phase, Volt Typhoon aptly demonstrates its craftiness by leveraging living-off-the-land techniques, particularly Windows Management Instrumentation (WMI) and PowerShell. They utilise the built-in tools wmic, ntdsutil, netsh, and PowerShell to perform their objectives, thereby evading detection and blending in with regular Windows systems and network activities. By doing so, they bypass endpoint detection and response (EDR) systems that would typically alert on the introduction of third-party applications.

### **Persistence**

##### **T1106 Native API**

Volt Typhoon, like many sophisticated threat actors, ensures that their access remains stable over time, even if a system restarts or a user logs out. They accomplish this by using a variety of persistence techniques. Notably, they’ve been observed using the native API to implement such persistence mechanisms.

### **Privilege Escalation**

##### **T1088 Bypass User Account Control**

To gain higher-level privileges on a compromised system, Volt Typhoon employs various privilege escalation techniques. They’ve been known to bypass User Account Control, a security feature of Windows, to gain elevated access. This allows them to execute processes with administrative privileges, giving them greater control over the system and enhancing their capabilities to perform malicious actions.

### **Defence Evasion**

##### **T1070 Indicator Removal on Host &amp; T1562.001 Impair Defenses: Disable or Modify Tools**

One of the most striking aspects of Volt Typhoon’s modus operandi is their ability to elude detection. They’ve been known to remove indicators of their presence on the host system and disable or modify security tools. This not only allows them to maintain access to compromised systems but also makes it challenging for security analysts to identify and remediate their intrusions.

### **Credential Access**

##### **T1003.003 OS Credential Dumping: NTDS**

In their quest to gain access to valuable resources, Volt Typhoon doesn’t shy away from stealing credentials. They’ve been observed exfiltrating the ntds.dit file, the main Active Directory (AD) database file, and the SYSTEM registry hive from Windows domain controllers. This action allows them to perform password cracking and potentially gain access to many user accounts within the network.

### **Discovery**

##### **T1082 System Information Discovery**

To get a lay of the land within a compromised network, Volt Typhoon performs system information discovery. They’ve been seen executing commands to gather information about local drives, including details such as drive letter, file system, free space, and drive size. The command uses a command prompt to execute a Windows Management Instrumentation Command Line (WMIC) query, collecting vital information about the storage devices on the local host.

### **Lateral Movement**

##### **T1021 Remote Services**

Once within a network, Volt Typhoon spreads to other systems to expand its foothold. They use remote services for lateral movement within the network, thereby gaining access to more systems and increasing the potential for data exfiltration.

### **Collection**

##### **T1005 Data from Local System**

During the collection phase, Volt Typhoon focuses on gathering valuable data from local systems. They selectively target files, databases, and other resources that contain the kind of information they’re interested in. Possible tools used in the collection are noted to be 7zip, a popular archive tool.

### **Command and Control**

##### **T1090 Proxy**

Volt Typhoon has been observed leveraging compromised small office/home office (SOHO) network devices as intermediate infrastructure to obscure their activity. Much of the command and control (C2) traffic originates from local ISPs in the victim’s geographic area, making it harder to trace back to the threat actors.

# **Strategic Targeting of Guam**

Guam, a tiny island in the western Pacific, has frequently found itself in the sights of superpowers. This is because of its strategic value as a US military station and because of its location at the confluence of the South China Sea and the Pacific Ocean. It is a critical military centre because of the presence of the Naval Base Guam and the Andersen Air Force Base. In the world of cyberspace, this geopolitical significance translates into Guam becoming a high-value target for state-sponsored cyber threat actors like Volt Typhoon.

In the case of Volt Typhoon, the group’s purported focus on Guam is telling. The actions of Volt Typhoon, which are connected to the People’s Republic of China, are an extension of China’s regional geopolitical objectives. It is well known that the Chinese government is interested in keeping an eye on and possibly interfering with US military operations, particularly in the Asia-Pacific region. Thus, cyber-espionage campaigns targeting Guam could provide valuable intelligence that feeds into these broader strategic objectives.

The potential threats that Volt Typhoon could pose in the future are multi-faceted. Their sophisticated tactics, such as living off-the-land techniques and exploiting public-facing applications, indicate that they have the capability to launch stealthy and persistent attacks. The threat group’s focus on critical infrastructure sectors—such as communications, construction, education, government, IT, manufacturing, maritime, transportation, and utilities—suggests potential disruption of essential services, theft of sensitive data, and compromising strategic assets.

Moreover, Volt Typhoon’s apparent ability to evolve and adapt its TTPs indicates a capacity for advanced threat development. This means that they could refine their methods or even diversify their targets in response to defensive measures or to align with changing strategic goals.

The potential for these threats underscores the need for robust cybersecurity measures, especially for high-value targets like Guam. It’s vital for organisations and governments to keep abreast of the evolving tactics of threat groups like Volt Typhoon, continuously updating their defences to protect their networks and critical infrastructure.

In conclusion, the cyber activities of Volt Typhoon offer a glimpse into the intertwined worlds of geopolitics and cyber espionage. The strategic targeting of Guam is a stark reminder that in the digital age, no location is too remote to be spared from the global chess game of power and influence.

# **Global Response**

The worldwide reaction to Volt Typhoon’s operations underlines the seriousness of this cyber threat. The U.S. Cybersecurity &amp; Infrastructure Security Agency (CISA) took the lead in addressing Volt Typhoon’s actions, collaborating with counterparts around the globe to provide a comprehensive analysis of the group’s tactics. What stands out here is the global unity in response to a threat that disregards geographical boundaries, affecting organisations worldwide.

Microsoft has played a crucial role in countering Volt Typhoon’s activities. Microsoft’s products are widely used as a significant player in the tech world, making it an essential participant in the defence against such threats. Using its vast resources in threat intelligence, Microsoft has been able to track and identify Volt Typhoon’s operations, implementing necessary patches and advising users on protective measures.

Microsoft and other security research companies are a crucial line of defence in our increasingly digital world. Their global reach allows them to detect, respond to, and mitigate cyber threats in unmatched ways. They work with government agencies and contribute to threat intelligence networks, providing vital support in managing complex cyber threats like Volt Typhoon.

This worldwide effort is a testament to what we can achieve when we work together to address cyber threats. It emphasises the importance of swift, collective action and public-private partnerships in bolstering cyber resilience. As we navigate a constantly evolving digital landscape, such cooperative efforts are vital in protecting our cyber infrastructure.

# **Final Summary**

In conclusion, the emergence and operations of Volt Typhoon, a state-sponsored APT group, have ushered in a new era of cyber threats that leverage sophisticated techniques to stay under the radar while carrying out malicious activities. Targeting critical infrastructure sectors worldwide and focusing on strategic locations like Guam, Volt Typhoon has indeed become a significant concern in the global cybersecurity landscape.

However, the collective response of global cybersecurity agencies and tech giants like Microsoft has shown that united efforts can significantly mitigate such threats. Their ongoing investigations and proactive measures have provided organisations with valuable insights and resources to strengthen their defences against Volt Typhoon’s operations.

In the next instalment of this blog series, I will be delving deeper into the technical aspects of Volt Typhoon’s methods. Through a lab demonstration, I aim to illustrate the inner workings of their attacks, offering a hands-on understanding of their tactics. Furthermore, we will explore the various strategies and practices that can be used to mitigate such attacks, providing actionable insights for organisations to enhance their cybersecurity posture.

Even as we conclude this part of the discussion, it’s important to remember that our understanding of Volt Typhoon continually evolves. I will persist in investigating and researching this threat actor, ensuring that the information provided in this blog remains current and relevant. Our vigilance and continuous learning in the face of such threats are indeed our best line of defence in the complex world of cybersecurity.

Stay tuned for Part 2, where we’ll delve deeper into the shadows of Volt Typhoon and shed light on how we can protect our digital landscape from such threats.
