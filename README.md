#Pi-Switch


##Introduction
This project is Pi Stack Switch for SDN & Programmable Network.
Pi Stack Switch is SDN Testbed using Raspberry Pi2 and OpenvSwitch.


##Installation
1. Set prerequisites
`$ sudo rpi-update`
`$ sudo apt-get update`


2. Install OpenvSwitch
`$ sudo apt-get install openvswitch-switch openvswitch-controller openvswitch-common openvswitch-brcompat ovsdbmonitor openvswitch-pki`


3. Add Network Interface(Hardware device) at Raspberry Pi. ex> USB to Ethernet adaptor


4. Check connection between Network Interface and Raspberry Pi
`$ ifconfig`


5. Configure OVS in Raspberry Pi
`$ sudo ovs-vsctl add-br <BridgeName>`
`$ sudo ifconfig <BridgeName> up`
`$ sudo ovs-vsctl add-port <BridgeName> eth0`
`$ sudo ovs-vsctl add-port <BridgeName> eth1`
...


6. If Your Pis are allocated IP address, Set IP address/netmask on bridge
[example]
`$ sudo ifconfig <BridgeName> 192.168.0.101/24`
`$ sudo ifconfig eth0 0`


7. Edit MAC address of Pi-eth0 and bridge's MAC address
`$ sudo ifconfig <BridgeName> hw ether 00:00:00:00:00:00`


8. Set controller of Pi Switch
`$ sudo ovs-vsctl set-controller <BridgeName> tcp:000.000.000.000:6633`



