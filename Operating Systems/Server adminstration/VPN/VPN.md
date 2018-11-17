- [PPTP](https://en.wikipedia.org/wiki/Point-to-Point_Tunneling_Protocol), port: TCP 1723 (maintenance traffic), [GRE protocol (IP protocol 47)](https://en.wikipedia.org/wiki/Generic_Routing_Encapsulation) (tunneled data to pass through router) **⚠️ PPTP is not recommended, it's not secured enough.**
- [SSTS](https://en.wikipedia.org/wiki/Secure_Socket_Tunneling_Protocol), port TCP 443
- [L2TP/IPSec](https://en.wikipedia.org/wiki/Layer_2_Tunneling_Protocol#L2TP.2FIPsec) (aka L2TP over IPSec), port: UDP 1701 (L2TP traffic) + same ports than IPSec
- [IPSec](https://en.wikipedia.org/wiki/IPsec) (aka Cisco IPSec), port [IKE](https://en.wikipedia.org/wiki/Internet_Key_Exchange): UDP 500, port [NAT](https://en.wikipedia.org/wiki/Network_address_translation): UDP 4500
- [IKEv2/IPSec](https://en.wikipedia.org/wiki/Internet_Key_Exchange#Improvements_with_IKEv2), same ports as IPSec **Recommended over IKEv1 for its ability to reconnect very quickly in the event that your VPN connection gets disrupted and strong encryption (AES 128, AES 192, AES 256)**
- [OpenVPN](https://en.wikipedia.org/wiki/OpenVPN), port UDP 1194

- [PPTP vs L2TP vs OpenVPN vs SSTP vs IKEv2 - BestVPN.com](https://www.bestvpn.com/blog/4147/pptp-vs-l2tp-vs-openvpn-vs-sstp-vs-ikev2/)
- [Setting up an L2TP/IPSec server on Debian - aa-asterisk.org.uk wiki](https://www.aa-asterisk.org.uk/Setting_up_an_L2TP/IPSec_server_on_Debian)
- [IPsec versus L2TP/IPsec - Super User](https://superuser.com/questions/378252/ipsec-versus-l2tp-ipsec)
- [2x HOW TO | OpenVPN](https://openvpn.net/community-resources/how-to/)

**If you local network use the same subnet as remote (through VPN) subnet, you could not reach devices on remote network.** Example: your local netowk use 192.168.1.0/24 subnet and the remote network (through VPN connection) use 192.168.1.0/24 subnet. Change one of network to use an other subnet (ex.: `192.168.2.0/24`). [How do you deal with VPN access that has the same subnet as your corporate environment? : sysadmin](https://www.reddit.com/r/sysadmin/comments/437y5p/how_do_you_deal_with_vpn_access_that_has_the_same/)

- [How to setup your own private, secure, free* VPN on the Amazon AWS Cloud in 10 minutes by Web Development](https://www.webdigi.co.uk/blog/2015/how-to-setup-your-own-private-secure-free-vpn-on-the-amazon-aws-cloud-in-10-minutes/) - see https://github.com/webdigi/AWS-VPN-Server-Setup

## Setup iOS client

- server
- id. distant : given when set up VPN server
- id. local : username
- type : aucun
- secret partagé : user's password

Or create a configuration profile manually https://wiki.strongswan.org/projects/strongswan/wiki/AppleIKEv2Profile or with [Apple Configurator](https://www.apple.com/support/iphone/business/)