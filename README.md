# L2-Link-Agg

##LACP

Link Aggregation Control Protocol (LACP) is part of an IEEE specification (802.3ad) that allows several physical ports to be bundled together to form a single logical channel.

The LACP modes of operation are as follows:
1. Active: Enable LACP unconditionally. It sends LACP requests to connected ports.
2. Passive: Enable LACP only if an LACP device is detected. It waits for LACP requests and responds to requests for LACP negotiation.

LACP can be Active - Active, Active - Passive, on - on. but can't Passive - Passive

###LACP Configuration
create the port-channel
```
SWICTH1# configure terminal
SWICTH1(config)# interface port-channel 10
```
assign physical port to LACP
```
SWICTH1# configure terminal
SWICTH1(config)# interface range fastethernet 0/0-1
SWICTH1(config-if)# channel-group 10 mode active
SWICTH1(config-if)# exit
```
```
SWICTH2# configure terminal
SWICTH2(config)# interface range fastethernet 0/0-1
SWICTH2(config-if)# channel-group 10 mode passive
SWICTH2(config-if)# exit
```

