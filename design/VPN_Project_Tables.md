# Site-to-Site IPsec VPN Configuration Documentation

## 1. Network Addressing Table
This table lists the logical addressing for all devices in the topology.

| Device | Interface | IP Address | Subnet Mask | Default Gateway | Connection / Port |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **R1** | G0/0 | 192.168.1.1 | 255.255.255.0 | N/A | S1 F0/1 |
| | S0/0/0 (DCE) | 10.1.1.2 | 255.255.255.252 | N/A | To R2 S0/0/0 |
| **R2** | G0/0 | 192.168.2.1 | 255.255.255.0 | N/A | S2 F0/2 |
| | S0/0/0 | 10.1.1.1 | 255.255.255.252 | N/A | To R1 S0/0/0 |
| | S0/0/1 (DCE) | 10.2.2.1 | 255.255.255.252 | N/A | To R3 S0/0/1 |
| **R3** | G0/0 | 192.168.3.1 | 255.255.255.0 | N/A | S3 F0/5 |
| | S0/0/1 | 10.2.2.2 | 255.255.255.252 | N/A | To R2 S0/0/1 |
| **PC-A** | NIC | 192.168.1.3 | 255.255.255.0 | 192.168.1.1 | S1 F0/2 |
| **PC-B** | NIC | 192.168.2.3 | 255.255.255.0 | 192.168.2.1 | S2 F0/1 |
| **PC-C** | NIC | 192.168.3.3 | 255.255.255.0 | 192.168.3.1 | S3 F0/18 |

---

## 2. ISAKMP Phase 1 Policy Parameters
These settings define the management tunnel used to negotiate the security association.

| Parameter | Configuration on R1 | Configuration on R3 |
| :--- | :--- | :--- |
| **Policy Number** | 10 | 10 |
| **Encryption Algorithm** | AES 256 | AES 256 |
| **Hash Algorithm** | SHA-1 | SHA-1 |
| **Authentication Method** | Pre-share | Pre-share |
| **Diffie-Hellman Group** | Group 5 | Group 5 |
| **IKE SA Lifetime** | 86400 seconds | 86400 seconds |
| **Pre-shared Key** | `vpnpa55` | `vpnpa55` |
| **Peer IP Address** | 10.2.2.2 | 10.1.1.2 |

---

## 3. IPsec Phase 2 Policy Parameters
These parameters define how the user data is encrypted and authenticated.

| Parameter | Configuration Value |
| :--- | :--- |
| **Transform Set Name** | VPN-SET |
| **ESP Transform Encryption** | esp-aes |
| **ESP Transform Authentication**| esp-sha-hmac |
| **Crypto Map Name** | VPN-MAP |
| **Sequence Number** | 10 |
| **SA Establishment** | ipsec-isakmp |

---

## 4. Interesting Traffic Identification (ACL 110)
Access Control Lists used to define which traffic triggers the VPN tunnel.

| Router | Source Network | Destination Network | Action |
| :--- | :--- | :--- | :--- |
| **R1** | 192.168.1.0/24 | 192.168.3.0/24 | Permit (Encrypt) |
| **R3** | 192.168.3.0/24 | 192.168.1.0/24 | Permit (Encrypt) |

---

## 5. Passwords & Credentials
Standard credentials used for device access during the project.

| Type | Username / Context | Password |
| :--- | :--- | :--- |
| **Console** | Line con 0 | `ciscoconpa55` |
| **VTY** | Line vty 0 4 | `ciscovtypa55` |
| **Enable** | Global | `ciscoenpa55` |
| **SSH** | SSHadmin | `ciscosshpa55` |
