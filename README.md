# openvpn

Set a static IP for Raspbian Jessie: https://www.modmypi.com/blog/how-to-give-your-raspberry-pi-a-static-ip-address-update

Automated script to setup openvpn for Raspbian Jessie: https://github.com/StarshipEngineer/OpenVPN-Setup
  
      1.Remove local <IP> line from /etc/openvpn/server.conf
      2.Change port in server.conf and in client.ovpn (OPTIONAL)
      3.Alter the push dchp command in server.conf to use the Pi/OPENNIC as DNS
      
Install PI-HOLE https://pi-hole.net/

To push dns server from openvpn to Ubuntu:http://serverfault.com/questions/528773/networkmanager-is-not-changing-etc-resolv-conf-after-openvpn-dns-push
