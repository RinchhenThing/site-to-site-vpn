# Understandings of the project's intial phase

## 1. DCE 
Data Circuit-Terminating Equipment (DCE) is a networking device that sits between the Data Terminal Equipment (DTE) and a data transmission circuit, serving as an interface to the network.  DCE devices are responsible for signal conversion, coding, and clocking to ensure data is transmitted reliably over the communication medium. 

The **DCE** device is reponsible for providing the **clock rate**. This signal synchronizes the timing of the data transmission between the two devices. In a rea-world scenario, the DCE is usually a modem or a CSU/DSU provided by the Service Provider (ISP).

In, Packet Tracer as we are connecting two routers directly (a back-to-back serial connection), one router must "pretend" to be service provider's equipment.

In the addressing table, R1 and R2 (S0/0/1) are marked as DCE. This means when we configure those specific interfaces in the CLI, we would need to specify the clock rate:

```bash
R1(config)# interface s0/0/0
R1(config-if)# clock rate 128000
```

**Note:** When we connect two routers via a serial cable, one end must act as the **"master"** and the other as the **"slave"** regarding the timing of the data transfer. 


## Routing 
I have set three routers
- home router
- ISP router 
- Office router

One PC is connected to each home and office router.

**Now** for those PCs to ping each other a route has to be set 

 ## On Home_Router:
  Tell it to send traffic for the Office network to the ISP.
  ```bash
```
  ip route 192.168.20.0 255.255.255.0 10.20.30.1
  ```
```

  ## On ISP_Router:
  The ISP needs to know where both "offices" are located.
  ```bash
```
  ip route 192.168.10.0 255.255.255.0 10.20.30.2
  ip route 192.168.20.0 255.255.255.0 10.20.40.2
  ```
```

  ## On Office_Router:
  Tell it to send traffic for the Home network back to the ISP.
```bash
```
  ip route 192.168.10.0 255.255.255.0 10.20.40.1
```
```

