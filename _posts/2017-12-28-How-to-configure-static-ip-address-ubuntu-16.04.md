
1. Firstly, you need to know about your "interfaces" look like such as: eth0, enp2s0
   To know that, type: $ ifconfig
   Here is the result
   >> enp2s0    Link encap:Ethernet
      ...
2. Edit /etc/network/interfaces
             $ sudo nano /etc/network/interfaces
3. A screen is displayed
--------------------------------------------------------------
# interfaces(5) file used by ifup(8) and ifdown(8)
auto lo
iface lo inet loopback
--------------------------------------------------------------
4. Modify like as follows:
--------------------------------------------------------------
# interfaces(5) file used by ifup(8) and ifdown(8)
auto lo
iface lo inet loopback
auto enp2s0
iface enp2s0 inet static
        address x.x.x.x # your_ip_address
        netmask 255.255.255.0 # netmask
        broadcast x.x.x.x # your_broadcasr
        gateway x.x.x.x #your_gate_way
        dns-nameservers 8.8.8.8 8.8.4.4 
        dns-search lan
-------------------------------------------------------------
#Save and exit
5. Implement the same way with another syntax:
$  sudo nano /etc/resolv.conf
Just add lines as below:
------------------------------------------------------------
nameserver 8.8.8.8
nameserver 8.8.4.4
search lan
------------------------------------------------------------
#Save and exit

6. Restart the networking service 
$ sudo /etc/init.d/networking restart
After doing that, if you don't get any errors, your network now be configured with the static IP address.
Finally, perform a reset by:
$ sudo reboot

That's it.
