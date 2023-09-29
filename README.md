# L2-Link-Agg

## LACP

Link Aggregation Control Protocol (LACP) is part of an IEEE specification (802.3ad) that allows several physical ports to be bundled together to form a single logical channel.

The LACP modes of operation are as follows:
1. Active: Enable LACP unconditionally. It sends LACP requests to connected ports.
2. Passive: Enable LACP only if an LACP device is detected. It waits for LACP requests and responds to requests for LACP negotiation.

LACP can be Active - Active, Active - Passive, on - on. but can't Passive - Passive

### LACP Configuration
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
configure each side.
## PAgP

Port Aggregation Protocol (PAgP) provides the same negotiation benefits as LACP. PAgP is a Cisco proprietary protocol, and it will only work on Cisco devices.

The PAgP modes of operation:
1. Desirable: Enable PAgP unconditionally. In other words, it starts sending negotiation messages to other ports.
2. Auto: Enable PAgP only if a PAgP device is detected. In other words, it waits for requests and responds to requests for PAgP negotiation, which reduces the transmission of PAgP packets.

PAgP can be Desirable - Desirable, Desirable - auto, on - on. but can't auto - auto

When a PAgP mode of auto or desirable is configured on a port, you also have the option of configuring either of the following operational parameters:

1. Non-silent: an EtherChannel bundle does not form until bidirectional connectivity has been confirmed. This parameter means that ports in the EtherChannel bundle must receive data, as well as be able to transmit data, in order for the bundle to form. This mode protects against unidirectional failures, where one of the transmit or receive links may fail. Such failures are common on fiber-based connections and can cause bridging loops

2. Silent: an EtherChannel bundle forms, even if data has not been received from the remote device. This mode is used when the switch is connected to a device that is not PAgP-capable and seldom, if ever, sends packets. An example of a silent partner is a file server or a packet analyzer that is not generating traffic. In this case, running PAgP on a physical port connected to a silent partner prevents that switch port from ever becoming operational; however, the silent setting allows PAgP to operate, to attach the interface to a channel group, and to use the interface for transmission.

By default, the PAgP desirable mode is running in the non-silent mode and PAgP auto mode is running in the silent mode. Cisco recommends that you do not modify the default silent or non-silent mode of operation.

### PAgP Configuration
create the port-channel
```
SWICTH1# configure terminal
SWICTH1(config)# interface port-channel 10
```
assign physical port to PAgP
```
SWICTH1# configure terminal
SWICTH1(config)# interface range fastethernet 0/0-1
SWICTH1(config-if)# channel-group 10 mode desirable
SWICTH1(config-if)# exit
```
```
SWICTH2# configure terminal
SWICTH2(config)# interface range fastethernet 0/0-1
SWICTH2(config-if)# channel-group 10 mode auto
SWICTH2(config-if)# exit
```

Last is verify the configuration with
```
SWICTH1# show etherchannel summary
SWICTH1# show etherchannel detail
SWICTH1# show etherchannel port-channel
SWICTH1# show interface port-channel 1

```
