#Work in Progress. Everything listed till now should work as a whole.
#Securing DNS on the Consumer Level using a Dedicated Home Server and OpenVPN 
##This guide should work without modifications on a clean [Raspbian Jessie lite install](https://www.raspberrypi.org/downloads/raspbian/) and an IPV4 network.
###Related Setup
1.	Incase of Dynamic Public IP, you have to create a hostname for your public IP that updates frequently so you can always access the OpenVPN network. There are a lot of free options you can use. I found [noip's](https://noip.com) update client to be somewhat lacking. I have since then changed to [ddnss.de](https://ddnss.de/) in conjunction with ddclient and it works like a charm.
2.	As described in Raspberry Pi Setup point 3.2.1 you have to disable the DHCP server in your router at that moment so that dnsmasq can take over. 

###Raspberry Pi Setup
1.	Set a static IP for Raspbian Jessie with this [guide](https://www.modmypi.com/blog/how-to-give-your-raspberry-pi-a-static-ip-address-update).

2.	Automated [script](https://github.com/StarshipEngineer/OpenVPN-Setup) to setup OpenVPN for Raspbian Jessie.
	1. Edit OpenVPN server configuration file with `sudo nano /etc/openvpn/server.conf` and remove the following lines:
		* `push "redirect-gateway def1"`
		* `local (YOUR_STATIC_IP_SETUP_ABOVE)`
		* `push "dhcp-options (2 lines)`
	2. Add this line to the above config to use your DNS Server from OpenVPN connected devices. 
		* `push "dhcp-option DNS 10.8.0.1"` 
      
3.	Install PI-HOLE https://pi-hole.net/.
	* Edit dnsmasq configuration file with `sudo nano /etc/dnsmasq.conf`.
	* Append `dhcp-range=192.168.0.20,192.168.0.150,72h`. 
		* To make this work you have to enter your router and disable it's own DHCP server.
		* By using the dnsmasq as DHCP server your DNS server gets pushed to all devices on the network.
  * Append `listen-address=127.0.0.1, 10.8.0.1`.
		* By adding this the DNS server is listening to queries from your network AND your OpenVPN connected devices.
      
4.	Enabling DNSSEC.
	1.	Use this [script](https://github.com/simonclausen/dnscrypt-autoinstall) to install DNSproxy 
		* I suggest using a resolver that supports DNSSEC
	2.	Edit the DNScrypt daemon configuration file with `sudo nano /etc/systemd/system/dnscrypt-autoinstall.conf`
		*	Change the port `53` in `DNSCRYPT_LOCALPORT=53` and `DNSCRYPT_LOCALPORT2=53` to a chosen free port of your choice. Mine is `5353`.
	3.	Edit the dnsmasq configuration files with `sudo nano /etc/dnsmasq.conf`.
		* Remove all lines similar to `server=<RANDOM_DNS_SERVER>`.
		* Append following lines:
			* `server=127.0.0.1#5353`
			* `server=127.0.0.2#5353`
			
5. 	Using obfsproxy and pluggable transports from the Tor Project to obfuscate vpn traffic #WIP

5. You can use this [test](https://dnsleaktest.com/) on all your devices to check if your DNS is working properly.
6. You can use this [test](http://dnssec.vs.uni-due.de/) on all your devices to check if DNSSEC is working properly.





