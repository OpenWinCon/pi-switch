#Pi-Switch

&nbsp;

&nbsp;


##What is Pi-Switch?
 __Pi-Switch__ is cost-effective switch for SDN networking testbed using Raspberry Pi2 and Open vSwitch. Pi-Switch can be controlled via the OpenFlow protocol because it is based on the Open vSwitch. Then, It is made with low-cost single board computer called Raspberry Pi. If you have Raspberry Pi and USB to Ethernet adapter, you can build easily your own testing environment for SDN networking. Raspberry Pi2 supports basically four USB ports. You can add USB to Ethernet adapter for expanding Ethernet ports(Network interfaces). As a result Pi-Switch has single built-in Ethernet port and four expanded Ethernet ports, total five Ethernet ports. If you need more Ethernet ports, you can use self-powered USB hub.

&nbsp;&nbsp;&nbsp;




##Pi Stack Switch
Single Pi-Switch has limitation of Ethernet port number and lack of processing power. If you test network performance with just single Pi-Switch that supports 4 or more Ethernet port using self-powered USB hub, you may experience performance degradation due to bottleneck situation in chip of Raspberry Pi. This is problem of hardware.
So, We propose __Pi Stack Switch__ for solving these problems. If you want to test network with 4 or more Ethernet ports, we recommend Pi Stack Switch. Pi Stack Switch is made of stacked Pi-Switch and comprised of single main switch and 3 or 4 sub switch. Classification of main switch and sub switch is based on physical position.

&nbsp;&nbsp;&nbsp;





##Hardware Component of Pi Stack Switch
![](https://github.com/MobileConvergenceLab/pi-switch/blob/master/img/pi-switch-component.jpg)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;




##Deployment of Main / Sub switch 
<img src="https://github.com/MobileConvergenceLab/pi-switch/blob/master/img/pi-switch-2.jpg" width="30%">
<img src="https://github.com/MobileConvergenceLab/pi-switch/blob/master/img/pi-switch-3.jpg" width="44%">
###Single main switch and three sub switch

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;




##Process
<img src="https://github.com/MobileConvergenceLab/pi-switch/blob/master/img/pi-switch-process.jpg">

※_[Caution] It may not function due to the difference in power consumption according to the type of the adapter's chipset._

---

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
    
    


6. If Your Pis are allocated IP address, Set IP address/netmask on bridge. And deallocate eth0.

    `$ sudo ifconfig <BridgeName> <IP address/subnet>`

    [example]
    `$ sudo ifconfig <BridgeName> 192.168.0.101/24`
    
    `$ sudo ifconfig eth0 0`
    
    


7. Edit MAC address of Pi-eth0 and bridge's MAC address (Pi-eth0 MAC addr == Bridge MAC addr)

    `$ sudo ifconfig <BridgeName> hw ether <MAC Address of Pi-eth0>`

    [example]
    `$ sudo ifconfig <BridgeName> hw ether 00:00:00:00:00:00`
    





8. Set controller of Pi Switch
  
    `$ sudo ovs-vsctl set-controller <BridgeName> tcp:000.000.000.000:6633`




