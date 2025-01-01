# DCCOR

Welcome to the **DCCOR 350-601 Not So Official Study Guide** repository. This repository is designed to help you prepare for the Cisco CCNP Data Center Core certification exam by providing structured materials, hands-on labs, and detailed topic breakdowns.

## Structure of the Repository

The repository is organized into branches to align with specific topics and chapters from the official study guide. Each branch contains:

- **Docs Folder:** Contains documentation, study notes, and reference materials for the topic.
    
- **Labs Folder:** Includes hands-on lab scenarios and configurations for practical practice.
    

## Groupings by Topic

### Part I: Networking

- **Branch 1:** `routing` (Chapter 1: Implementing Routing in the Data Center)
    - Topics include: Routing protocols (RIP, OSPF, EIGRP, BGP), route redistribution, policy-based routing, and basic routing configuration in the data center environment.
- **Branch 2:** `switching-protocols` (Chapter 2: Implementing Data Center Switching Protocols)
    - Topics include: Layer 2 switching protocols, VLANs, VTP, Spanning Tree Protocol (STP), EtherChannel, and advanced Layer 2 designs for the data center.
- **Branch 3:** `overlay-protocols` (Chapter 3: Implementing Data Center Overlay Protocols)
    - Topics include: VXLAN, NVGRE, overlay networking concepts, and configuration of overlay protocols in a data center environment.
- **Branch 4:** `aci-overview` (Chapter 4: Describe Cisco Application Centric Infrastructure)
    - Topics include: Overview of Cisco ACI architecture, key components such as APIC, leaf/spine architecture, and the role of application profiles and policies.
- **Branch 5:** `cloud-services` (Chapter 5: Cisco Cloud Services and Deployment Models)
    - Topics include: Hybrid and multi-cloud architectures, Cisco cloud services, and the deployment of cloud-based data centers.
- **Branch 6:** `network-management` (Chapter 6: Data Center Network Management and Monitoring)
    - Topics include: Data center network monitoring tools, SNMP, NetFlow, and other network management practices for ensuring network health and performance.
- **Branch 7:** `nexus-dashboard` (Chapter 7: Describe Cisco Nexus Dashboard)
    - Topics include: Cisco Nexus Dashboard architecture, integration with ACI, and how to use Nexus Dashboard to manage data center network infrastructure.

---

### Part II: Storage

- **Branch 8:** `fibre-channel` (Chapter 8: Implement Fibre Channel)
    
    - Topics include: Fibre Channel (FC) protocol, zoning, virtual SANs, and Fibre Channel configuration in the data center environment.
- **Branch 9:** `fcoe` (Chapter 9: Implement FCoE Unified Fabric)
    
    - Topics include: Fibre Channel over Ethernet (FCoE) protocol, FCoE configuration, and integrating Ethernet and Fibre Channel networks.
- **Branch 10:** `nfs-nas` (Chapter 10: Describe NFS and NAS Concepts)
    
    - Topics include: Network File System (NFS), Network Attached Storage (NAS), file sharing protocols, and configurations for implementing storage solutions in a data center.
- **Branch 11:** `storage-monitoring` (Chapter 11: Describe Software Management and Infrastructure Monitoring)
    
    - Topics include: Storage monitoring tools, software management practices, and the role of monitoring in data center storage.

---

### Part III: Compute

- **Branch 12:** `ucs-overview` (Chapter 12: Cisco Unified Computing Systems Overview)
    - Topics include: Cisco UCS architecture, components such as fabric interconnects, blades, and rack servers, and the UCS management interface.
- **Branch 13:** `ucs-monitoring` (Chapter 13: Cisco Unified Computing Infrastructure Monitoring)
    - Topics include: Monitoring of UCS environments, integration with Cisco Prime Infrastructure, and performance monitoring tools.
- **Branch 14:** `ucs-management` (Chapter 14: Cisco Unified Compute Software and Configuration Management)
    - Topics include: UCS Manager, UCS Director, software management and automation in UCS environments.
- **Branch 15:** `hyperflex` (Chapter 15: Cisco HyperFlex Overview)
    - Topics include: Cisco HyperFlex architecture, configuration, and how it integrates compute, storage, and networking into a hyper-converged infrastructure.

---

### Part IV: Automation

- **Branch 16:** `automation-tools` (Chapter 16: Automation and Scripting Tools)
    - Topics include: Tools for automation, such as Ansible, Python, and other scripting languages, as well as network automation practices for data center environments.
- **Branch 17:** `orchestration` (Chapter 17: Evaluate Automation and Orchestration Technologies)
    - Topics include: Orchestration frameworks, such as Cisco CloudCenter and Cisco ACI, and how automation integrates with network orchestration for cloud environments.

---

### Part V: Security

- **Branch 18:** `network-security` (Chapter 18: Network Security)
    - Topics include: Security protocols, firewalls, VPNs, and intrusion detection systems (IDS/IPS) in the data center network.
- **Branch 19:** `compute-security` (Chapter 19: Compute Security)
    - Topics include: Securing compute resources, server hardening, and security protocols to protect data and applications running in data centers.
- **Branch 20:** `storage-security` (Chapter 20: Storage Security)
    - Topics include: Protecting storage systems, encryption methods, and securing access to data in data center storage environments.

---

### Final Preparation

- **Branch 21:** `final-preparation` (Chapter 21: Final Preparation)
    - Topics include: Tips for final exam preparation, review of all exam objectives, and test-taking strategies.
- **Branch 22:** `exam-updates` (Chapter 22: CCNP and CCIE Data Center Core DCCOR 350-601 Official Cert Guide Exam Updates)
    - Topics include: Latest updates to the exam content, changes in the exam format, and additional resources for last-minute preparation.
## Tools and Lab Environment

To simulate and practice the concepts covered in this guide, the following tools will be used:

### GNS3 Settings

|**Device**|**Routing Protocols Supported**|
|---|---|
|**Dynamips**|RIP, OSPF, EIGRP, BGP|
|**IOL**|RIP, OSPF, EIGRP, BGP|
|**VyOS**|RIP, OSPF, BGP|
|**Mikrotik CHR**|RIP, OSPF, BGP|
|**FRRouting/Quagga**|RIP, OSPF, BGP|
|**Linux VMs**|RIP, OSPF, BGP|

### Additional Tool

- **Cisco Packet Tracer** will also be used to reinforce concepts and provide additional practice opportunities.
    

## Getting Started

1. Clone this repository to your local machine.
    
2. Checkout the branch corresponding to the topic you want to study.
    
    ```
    git checkout <branch-name>
    ```
    
3. Explore the `Docs` and `Labs` folders for materials and labs.
    
4. Follow the weekly study plan to progress through the topics systematically.
    

## Contributing

We welcome contributions to improve the configuration or documentation. Follow these steps:

1. Fork the repository
2. Create a new branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request
## Resources

- [Official Cisco Study Guide](https://www.cisco.com)
    
- [Cisco Learning Network](https://learningnetwork.cisco.com)
    

