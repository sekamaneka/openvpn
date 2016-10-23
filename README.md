# openvpn

Set a static IP for Raspbian Jessie: https://www.modmypi.com/blog/how-to-give-your-raspberry-pi-a-static-ip-address-update

Automated script to setup openvpn for Raspbian Jessie: https://github.com/StarshipEngineer/OpenVPN-Setup
  
      1.Remove local <IP> line from /etc/openvpn/server.conf
      2.Remove push "redirect-gateway def1"
      2.Change port in server.conf and in client.ovpn (OPTIONAL)
      3.Remove all the push "dhcp-options and enter this: push "dhcp-option DNS 10.8.0.1" to use the dnsmasq 
      
Install PI-HOLE https://pi-hole.net/
      
      1. Edit /etc/dnsmasq.d/01-pihole.conf and add/edit 2,3.
      2. dhcp-range=192.168.0.20,192.168.0.50,72h. Using dnsmasq as dhcp server lets you push the dns to all network devices including openvpn connected ones.
      3. listen-address=127.0.0.1, 10.8.0.1 #needed for above so that dnsmasq listens to queries from vpn network
      

If you want to enable dnscrypt with your pi-hole:

      1. Use this script to install dnsproxy https://github.com/simonclausen/dnscrypt-autoinstall
      2. Change the default port to something else(I use 5353) because it's the same as dnsmasq. sudo vi /etc/systemd/system/dnscrypt-autoinstall.conf
      3. Change the server value in /etc/dnsmasq.d/01-pihole.conf to the ones listed in the above conf script





