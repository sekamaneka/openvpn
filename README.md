# openvpn

Set a static IP for Raspbian Jessie: https://www.modmypi.com/blog/how-to-give-your-raspberry-pi-a-static-ip-address-update

Automated script to setup openvpn for Raspbian Jessie: https://github.com/StarshipEngineer/OpenVPN-Setup
  
      1.Remove local <IP> line from /etc/openvpn/server.conf
      2.Change port in server.conf and in client.ovpn (OPTIONAL)
      3.Alter the push dchp command in server.conf to use the Pi as DNS server with dnsmasq(below)
      4.To push dns server from openvpn to Ubuntu:          
        http://serverfault.com/questions/528773/networkmanager-is-not-changing-etc-resolv-conf-after-openvpn-dns-push
      
Install PI-HOLE https://pi-hole.net/
      
      1. Change DNS servers away from GDNS: edit /etc/dnsmasq.d/01-pihole.conf and modify the server= values along with 2,3.
      2. dhcp-range=192.168.0.20,192.168.0.50,72h. Using dnsmasq as dhcp server lets you push the dns to all network devices including openvpn connected ones.
      3. listen-address=127.0.0.1, 10.8.0.1 #needed for above so that dnsmasq listens to queries from vpn network





