
### Scenario: BGP Implementation in the Data Center

### Overview

In this scenario, you are tasked with configuring **BGP (Border Gateway Protocol)** as the primary routing protocol for interconnecting multiple data center routers and integrating with external networks. The goal is to create a resilient, scalable BGP design that supports both external and internal routing, while implementing features like route filtering, prefix lists, and BGP attributes to optimize the routing decision process.

You will configure BGP between different routers in the data center, ensure efficient route advertisement and acceptance, and implement various BGP features like **Route Reflectors**, **AS Path Prepending**, **Prefix Lists**, **BGP Peering**, and **BFD for fast convergence**.

### Network Design

- **Core Router (R1):** The primary router that peers with external ISPs (via EBGP) and internal routers (via IBGP). R1 serves as the main point of contact for the data center’s BGP routing.
- **Internal Routers (R2, R3, R4):** These routers connect the core to the distribution and access layers of the data center. They participate in IBGP within the internal AS.
- **External ISP Routers (R5):** Routers that connect the data center to external ISPs via EBGP.
- **Edge Routers (R6, R7):** Routers that connect internal data center networks to external networks and Internet, receiving routes via EBGP from external ISPs.

### Requirements

1. **IP Addressing:**
    
    - R1: 10.1.1.1/30 (Core Router Interface)
    - R2: 10.1.1.2/30 (Internal Router 1)
    - R3: 10.1.1.3/30 (Internal Router 2)
    - R4: 10.1.1.4/30 (Internal Router 3)
    - R5: 10.1.1.5/30 (ISP Router 1)
    - R6: 10.1.1.6/30 (Edge Router 1)
    - R7: 10.1.1.7/30 (Edge Router 2)
    - Internal Network: 192.168.1.0/24
    - External Network: 203.0.113.0/24
2. **BGP Configuration:**
    
    - Internal Autonomous System (AS): **65001**
    - External Autonomous System (AS): **64512** for ISP Routers.
    - BGP peering between **R1 and R5** (EBGP).
    - IBGP peering between **R1, R2, R3, and R4** in AS 65001.
3. **BGP Peering:**
    
    - **EBGP** between R1 and R5 (ISP router) to exchange routes with external networks.
    - **IBGP** between R1, R2, R3, and R4 to share routing information within the internal network (AS 65001).
4. **BGP Route Filtering:**
    
    - Apply **prefix lists** on R1 to filter out any unwanted prefixes coming from external ISP (R5).
    - Ensure that only specific prefixes are advertised to external ISP via BGP.
5. **AS Path Prepending:**
    
    - Configure **AS Path Prepending** on R2 to make routes from R2 less preferred when advertised to R5.
6. **BGP Route Reflection (Optional):**
    
    - Set up a **BGP Route Reflector** on R1 to simplify IBGP peering between R2, R3, and R4 without requiring full mesh IBGP connections.
7. **BFD (Bidirectional Forwarding Detection):**
    
    - Enable **BFD** on the EBGP session between R1 and R5 for faster convergence.
8. **BGP Attributes (Optional):**
    
    - Use **local preference** on R1 to prefer routes received from a certain internal router over others.
9. **Route Advertisement:**
    
    - Ensure that **R1 advertises** the internal networks (192.168.1.0/24) to the external ISP (R5) using BGP.
    - Ensure that **R2, R3, and R4** are able to receive routes from R1 and make the best routing decisions for their internal networks.
10. **Default Route Propagation:**
    

- Advertise a **default route** from R1 to the internal routers (R2, R3, R4) via IBGP so that these routers can route traffic to external networks.

### Tasks to Accomplish

1. **Configure BGP on R1 (Core Router):**
    
    - Enable **BGP** with **AS 65001** on R1.
    - Set up **EBGP peering** between R1 and R5 with AS 64512.
    - Configure **IBGP** peering with R2, R3, and R4.
    - Advertise internal networks (192.168.1.0/24) to external ISP via EBGP.
    - Apply **prefix lists** to filter incoming prefixes from R5.
    - Advertise a **default route** (0.0.0.0/0) to the internal routers via IBGP.
2. **Configure BGP on R5 (ISP Router):**
    
    - Enable **BGP** with **AS 64512** on R5.
    - Set up **EBGP peering** between R5 and R1 (AS 65001).
    - Advertise external networks (203.0.113.0/24) to R1.
3. **Configure IBGP on R2, R3, and R4 (Internal Routers):**
    
    - Enable **BGP** on each router with **AS 65001**.
    - Set up **IBGP peering** between R2, R3, R4, and R1.
    - Ensure that R2, R3, and R4 receive routing information from R1 and use it to route internal traffic.
4. **Implement AS Path Prepending (Optional):**
    
    - On R2, apply **AS Path Prepending** to make the routes from R2 less preferred when advertised to R5.
5. **Configure Route Reflection (Optional):**
    
    - On R1, configure it as the **Route Reflector** to simplify IBGP peering between R2, R3, and R4.
    - Configure **R2, R3, and R4** as **Route Reflector Clients**.
6. **Enable BFD for Fast Convergence:**
    
    - On the **EBGP session** between R1 and R5, enable **BFD** to detect failures more quickly and improve convergence time.
7. **Verification and Troubleshooting:**
    
    - Verify **BGP peering** status with `show ip bgp summary` to ensure all BGP sessions are up.
    - Verify **BGP routes** with `show ip bgp` and ensure that the correct routes are being exchanged.
    - Verify **BGP table** with `show ip route bgp` to ensure that routes are correctly propagated.
    - Use **`ping`** and **`traceroute`** to confirm end-to-end connectivity, especially for external routes.
    - Verify **prefix filtering** by checking the prefixes received from R5 using `show ip bgp neighbors`.
    - Use **`show ip bgp path`** to check for **AS Path Prepending** and confirm that R2’s routes are less preferred.

### Expected Outcome

- **BGP Peering:** R1 should have successful BGP peering with R5 (EBGP) and R2, R3, and R4 (IBGP), ensuring the exchange of routing information.
- **Secure Route Filtering:** Only the desired prefixes from R5 should be accepted, and only the correct prefixes should be advertised to the external ISP.
- **Optimized Routing:** The AS Path Prepending feature will ensure that R2’s routes are less preferred for external traffic, while the default route will provide a fallback option.
- **Fast Convergence:** BFD will enable fast failure detection, improving BGP convergence times.
- **Route Reflection:** The BGP Route Reflector setup will simplify the IBGP mesh, reducing the number of required peerings in larger networks.