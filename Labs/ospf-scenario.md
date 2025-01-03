# Scenario: OSPF Implementation in the Data Center

## Overview

In this scenario, you are tasked with implementing OSPF (Open Shortest Path First) as the primary routing protocol within a data center environment. The goal is to create a resilient, scalable, and efficient OSPF network to interconnect multiple routers across various layers of the data center.

You will configure OSPF on all routers in the network, ensure proper OSPF area configuration, and optimize the OSPF network to support efficient routing between devices. Additionally, you'll work with route summarization, OSPF authentication, and verification tasks to ensure optimal operation.

### Network Design

- **Core Router (R1):** The main router connecting different distribution routers and handling inter-area OSPF routing.
- **Distribution Routers (R2, R3):** Routers that connect access switches and aggregate traffic from multiple access routers.
- **Access Routers (R4, R5):** Edge routers responsible for routing traffic from devices in different VLANs.
- **Server VLAN (VLAN 10):** Used for data center server connectivity.
- **Management VLAN (VLAN 20):** For management and monitoring.
- **Storage VLAN (VLAN 30):** For storage devices.
- **Internet Router (R6):** A router connecting the data center to external networks.

### Requirements

1. **IP Addressing:**
    
    - R1: 192.168.1.1/24 (Management interface)
    - R2: 192.168.2.1/24 (Core distribution interface)
    - R3: 192.168.3.1/24 (Core distribution interface)
    - R4: 192.168.10.1/24 (Server subnet)
    - R5: 192.168.20.1/24 (Management subnet)
    - VLAN 10: 192.168.10.0/24
    - VLAN 20: 192.168.20.0/24
    - VLAN 30: 192.168.30.0/24
2. **OSPF Areas:**
    
    - **Area 0 (Backbone Area):** R1, R2, R3, and R6 should be part of Area 0 (backbone area).
    - **Area 1:** R4 and R5 should belong to Area 1 for isolated routing between application and management networks.
3. **OSPF Configuration:**
    
    - Configure **OSPF** on R1, R2, R3, R4, R5, and R6.
    - Use OSPF **Area 0** as the backbone area for inter-area routing.
    - Configure **Area 1** for the server and management network.
    - Set router priorities to ensure **DR/BDR** (Designated Router / Backup Designated Router) election for efficiency in broadcast segments.
4. **OSPF Authentication:**
    
    - Configure **OSPF authentication** using plaintext or MD5 authentication between routers in each area to secure OSPF communication.
5. **OSPF Route Summarization:**
    
    - Implement **route summarization** on R2 and R3 to aggregate multiple subnets into a single summarized route to reduce routing table size.
6. **OSPF Redistribution (Optional):**
    
    - Optionally, configure **redistribution** between OSPF and static or connected routes on R1 to ensure external routes are injected into the OSPF routing domain.
7. **OSPF Stub Area (Optional):**
    
    - Configure **Area 1** as a stub area on R4 and R5 to limit the type of LSAs (Link State Advertisements) sent between these routers and reduce OSPF overhead.
8. **Default Route Configuration:**
    
    - Configure a **default route** on R6 to propagate it throughout the OSPF domain using a default summary address.
    - Advertise this default route in OSPF to all routers.

### Tasks to Accomplish

1. **Configure OSPF on R1 (Core Router):**
    
    - Enable OSPF on R1 for Area 0.
    - Advertise the networks (192.168.1.0/24) and (192.168.2.0/24) within Area 0.
2. **Configure OSPF on R2 (Distribution Router):**
    
    - Enable OSPF for Area 0 and add networks in Area 0 (192.168.2.0/24).
    - Set router priority on R2 to make it the DR on the segment with R1.
3. **Configure OSPF on R3 (Distribution Router):**
    
    - Enable OSPF for Area 0 and add networks in Area 0 (192.168.3.0/24).
    - Configure OSPF on R3 to be the BDR on the segment with R1 and R2.
4. **Configure OSPF on R4 and R5 (Access Routers):**
    
    - Enable OSPF for Area 1 on both R4 and R5, configuring these routers with the server and management networks (192.168.10.0/24 and 192.168.20.0/24).
    - Ensure OSPF routing works between R4, R5, and other routers in Area 0 through R1 and R2.
5. **Configure OSPF on R6 (Internet Router):**
    
    - Enable OSPF on R6 for Area 0.
    - Ensure routing between R6 and other routers in Area 0.
6. **OSPF Authentication:**
    
    - Configure OSPF authentication between routers in Area 0 (R1, R2, R3, R6) and between routers in Area 1 (R4, R5).
    - Implement either plaintext or MD5 authentication depending on the security requirements.
7. **Configure Route Summarization:**
    
    - Configure route summarization on R2 and R3 to aggregate the 192.168.10.0/24 and 192.168.20.0/24 networks into a summarized address such as 192.168.10.0/23.
    - This will reduce the number of routes advertised across the OSPF domain.
8. **Configure OSPF Stub Area (Optional):**
    
    - Configure **Area 1** as a stub area on R4 and R5 to limit LSAs and reduce the overhead of maintaining a full OSPF database.
9. **Redistribution (Optional):**
    
    - On R1, configure redistribution of static or connected routes into OSPF to ensure external routes are advertised to OSPF routers.
10. **Default Route Propagation:**
    

- Configure a default route on R6 (Internet Router).
- Advertise the default route throughout OSPF using `default-information originate` to ensure all routers can route to the external network.

11. **Verification and Troubleshooting:**

- Verify OSPF adjacencies using `show ip ospf neighbor`.
- Verify OSPF routes with `show ip route ospf` and ensure the routing tables are populated correctly.
- Check OSPF areas and configurations using `show ip ospf` and `show ip ospf interface`.
- Use `ping` and `traceroute` to confirm end-to-end connectivity.

### Expected Outcome

- **OSPF Routing:** All routers should successfully exchange OSPF routing information and maintain correct routing tables.
- **Secure OSPF Communication:** OSPF authentication will prevent unauthorized OSPF updates and ensure secure routing updates.
- **Efficient Routing:** Route summarization will reduce the size of the OSPF routing table and ensure more efficient routing in the data center.
- **High Availability:** Proper OSPF configurations on core and distribution routers will provide redundancy and resilience in case of router failures.
- **Optimized Network:** Stub areas and default route propagation will reduce unnecessary OSPF overhead and ensure that traffic flows optimally across the data center.


---


# Solution 

You will configure OSPF on all routers in the network, ensure proper OSPF area configuration, and optimize the OSPF network to support efficient routing between devices. Additionally, you'll work with route summarization, OSPF authentication, and verification tasks to ensure optimal operation.

## Network Design

|**Device**|**Role**|**OSPF Area**|**Purpose**|
|---|---|---|---|
|VyOS Router 1|Core Router (R1)|Area 0|Connects distribution routers|
|MikroTik CHR|Distribution Router (R2)|Area 0|Aggregates traffic from access routers|
|FRRouting/Quagga|Distribution Router (R3)|Area 0|Backup distribution router|
|VyOS Router 2|Access Router (R4)|Area 1|Handles server subnet (VLAN 10)|
|VyOS Router 3|Access Router (R5)|Area 1|Handles management subnet (VLAN 20)|
|Linux VM|Host Device|-|Traffic testing and verification|
|MikroTik CHR|Internet Router (R6)|Area 0|Connects to external networks|

---

## IP Addressing Plan

|   |   |   |   |   |
|---|---|---|---|---|
|**Device**|**Interface**|**IP Address**|**Subnet**|**Description**|
|R1|eth0|192.168.1.1|255.255.255.0|Management Interface|
|R2|eth0|192.168.2.1|255.255.255.0|Core Distribution|
|R3|eth0|192.168.3.1|255.255.255.0|Core Distribution|
|R4|eth0|192.168.10.1|255.255.255.0|Server VLAN|
|R5|eth0|192.168.20.1|255.255.255.0|Management VLAN|
|R6|eth0|192.168.30.1|255.255.255.0|Internet Connection|

---

## OSPF Area Design

|   |   |   |
|---|---|---|
|**Area**|**Routers**|**Description**|
|Area 0|R1, R2, R3, R6|Backbone Area for inter-area routing|
|Area 1|R4, R5|Stub area for server and management subnets|

---

## Step 1: OSPF Configuration

### Configure OSPF on Core Router (R1)

```
set interfaces ethernet eth0 address 192.168.1.1/24
set protocols ospf area 0 network 192.168.1.0/24
set protocols ospf parameters router-id 1.1.1.1
commit
save
```

### Configure OSPF on Distribution Router (R2)

```
set interfaces ethernet eth0 address 192.168.2.1/24
set protocols ospf area 0 network 192.168.2.0/24
set protocols ospf parameters router-id 2.2.2.2
commit
save
```

### Configure OSPF on Distribution Router (R3)

```
set interfaces ethernet eth0 address 192.168.3.1/24
set protocols ospf area 0 network 192.168.3.0/24
set protocols ospf parameters router-id 3.3.3.3
commit
save
```

### Configure OSPF on Access Router (R4)

```
set interfaces ethernet eth0 address 192.168.10.1/24
set protocols ospf area 1 network 192.168.10.0/24
set protocols ospf parameters router-id 4.4.4.4
set protocols ospf area 1 stub
commit
save
```

### Configure OSPF on Access Router (R5)

```
set interfaces ethernet eth0 address 192.168.20.1/24
set protocols ospf area 1 network 192.168.20.0/24
set protocols ospf parameters router-id 5.5.5.5
set protocols ospf area 1 stub
commit
save
```

### Configure OSPF on Internet Router (R6)

```
set interfaces ethernet eth0 address 192.168.30.1/24
set protocols ospf area 0 network 192.168.30.0/24
set protocols ospf parameters router-id 6.6.6.6
commit
save
```

---

## Step 2: Configure DR/BDR Elections

- Set R2 as the DR and R3 as the BDR for Area 0.
    
- Use the following command to verify DR/BDR status:
    

```
show ip ospf neighbor
```

---

## Step 3: OSPF Authentication

### Enable MD5 Authentication on R1

```
set protocols ospf area 0 authentication message-digest
set protocols ospf message-digest-key 1 md5 password secret123
commit
save
```

### Enable MD5 Authentication on R2, R3, R4, R5, and R6

Repeat the same commands with the corresponding IP addresses and router IDs.

---

## Step 4: Route Summarization

- On R2 and R3, configure route summarization to reduce the number of routes advertised across the OSPF domain.
    

```
set protocols ospf area 0 range 192.168.10.0/23
commit
save
```

---

## Step 5: Default Route Propagation

### Configure Default Route on R6

```
set protocols static route 0.0.0.0/0 next-hop 192.168.30.2
set protocols ospf default-information originate
commit
save
```

---

## Verification Commands

|                         |                                                  |
| ----------------------- | ------------------------------------------------ |
| **Command**             | **Description**                                  |
| `show ip ospf neighbor` | Check OSPF neighbor relationships                |
| `show ip route ospf`    | View OSPF routes in the routing table            |
| `show ip ospf`          | Verify OSPF configuration details                |
| `ping`                  | Test connectivity between routers                |
| `traceroute`            | Verify the path packets take through the network |
