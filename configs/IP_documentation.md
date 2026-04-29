# IP Documentation

## Devices in the Topology

### Home Network
- Home_Router
- Home_Switch
- PC_hm

### ISP
- Impersonating_ISP_Router

### Office Network
- Office_Router
- Office_Switch
- PC_off

---

## Network Subnets

| Network Description                         | Subnet            |
|--------------------------------------------|-------------------|
| Home Network                               | 192.168.10.0/24   |
| Office Network                             | 192.168.20.0/24   |
| Home Router ↔ ISP Connection               | 10.20.30.0/30     |
| Office Router ↔ ISP Connection             | 10.20.40.0/30     |


##  IP Address Assignment

| Device                  | Interface        | IP Address     | Subnet Mask     | Default Gateway   |
|-------------------------|------------------|----------------|------------------|-------------------|
| Home_Router             | G0/0             | 192.168.10.1   | 255.255.255.0    | N/A               |
| Home_Router             | S0/1/0           | 10.20.30.1     | 255.255.255.252  | N/A               |
| PC_hm                   | NIC              | 192.168.10.10  | 255.255.255.0    | 192.168.10.1      |
| Office_Router           | G0/0             | 192.168.20.1   | 255.255.255.0    | N/A               |
| Office_Router           | S0/1/0           | 10.20.40.1     | 255.255.255.252  | N/A               |
| PC_off                  | NIC              | 192.168.20.10  | 255.255.255.0    | 192.168.20.1      |
| ISP_Router              | S0/1/0 (to Home) | 10.20.30.2     | 255.255.255.252  | N/A               |
| ISP_Router              | S0/1/1 (to Office)| 10.20.40.2    | 255.255.255.252  | N/A               |
