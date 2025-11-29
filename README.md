# cisco-intervlan-network
corporate network demonstrating Inter-VLAN Routing and security policy enforcement using Cisco ACLs

## 🗺️ Network Topology & IP Addressing Scheme
<img width="840" height="486" alt="Screenshot 2025-11-29 at 1 32 54 AM" src="https://github.com/user-attachments/assets/62b6e79d-010a-4b67-b95e-c786c0a3349a" />

| Department | VLAN ID | Network Address | Default Gateway |
| :--- | :--- | :--- | :--- |
| **IT** | 10 | 192.168.10.0/24 | 192.168.10.1 |
| **HR** | 20 | 192.168.20.0/24 | 192.168.20.1 |
| **GUEST** | 30 | 192.168.30.0/24 | 192.168.30.1 |
| **Server** | 99 | 192.168.99.0/24 | 192.168.99.1 |

## ⚙️ Security Policy Implemented

The following security rules were enforced using **Extended ACLs** applied to the router's sub-interfaces:

| Policy | Source Network | Destination Network | Action |
| :--- | :--- | :--- | :--- |
| **HR Isolation** | HR (192.168.20.0) | Server (192.168.99.0) | DENY (Blocks HR access to the server farm) |
| **Guest Isolation** | Guest (192.168.30.0) | IT/HR (All internal) | DENY (Blocks Guest from accessing corporate resources) |

## Verification & Test Results

The project was  verified by testing  traffic flows:

1.  **SUCCESS:** IT PC (192.168.10.10) can ping HR PC (192.168.20.10). *(Proves Inter-VLAN Routing works)*
   <img width="324" height="143" alt="Screenshot 2025-11-29 at 1 39 54 AM" src="https://github.com/user-attachments/assets/980ed515-da3c-4471-ad32-ef263e67d362" />

   
3.  **SUCCESS:** IT PC (192.168.10.10) can ping the Server (192.168.99.10).
   <img width="324" height="130" alt="Screenshot 2025-11-29 at 1 41 06 AM" src="https://github.com/user-attachments/assets/728f2bb6-3c3a-4d93-a1a8-0ec772aebc13" />


5.  **FAILURE:** HR PC (192.168.20.10) fails to ping the Server (192.168.99.10). 
<img width="295" height="152" alt="Screenshot 2025-11-28 at 4 37 17 AM" src="https://github.com/user-attachments/assets/a82c418c-66bd-4332-a7aa-235c0c70a2d8" />

   
7.  **FAILURE:** GUEST PC (192.168.30.10) fails to ping IT PC (192.168.10.10).
   <img width="295" height="152" alt="Screenshot 2025-11-28 at 4 38 53 AM" src="https://github.com/user-attachments/assets/054409aa-cb19-4871-b4fd-aacaacbccd88" />


---
**Files in this Repository:**
* `Cisco__multi-vlan.pkt` 
* `access-list.txt` 
