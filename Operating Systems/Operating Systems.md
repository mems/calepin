## Desktop sharing

- [Virtual Network Computing — Wikipedia](https://en.wikipedia.org/wiki/Virtual_Network_Computing)
- [Comparison of remote desktop software — Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_remote_desktop_software)
- [Desktop sharing — Wikipedia](https://en.wikipedia.org/wiki/Desktop_sharing)

## Tablet kiosk mode

- [iOS](iOS#tablet-kiosk-mode)
- [Android](Android#tablet-kiosk-mode)

## Network Link Aggregation and aggregate the bandwidth

Use protocol LACP, need same router (connections to same devices at both ends)

- [OS X Yosemite: Combine Ethernet ports](https://support.apple.com/kb/PH18560?locale=en_US)
- [Link aggregation — Wikipedia](https://en.wikipedia.org/wiki/Link_aggregation)
- [Network Load Balancing — Wikipedia](https://en.wikipedia.org/wiki/Network_Load_Balancing)
- [networking - If I have two internet connections on osx, how can I use both to increase my bandwidth? - Super User](http://superuser.com/questions/363843/if-i-have-two-internet-connections-on-osx-how-can-i-use-both-to-increase-my-ban)

## Block Youtube IP

Because this IP has restricted bandwidth by your ISP. Force Youtube to use an other IP

### Mac OSX

Add rule

	sudo /sbin/ipfw add 01000 deny ip from any to 173.194.52.0/22

Display rules

	sudo /sbin/ipfw show

Delete rule

	sudo /sbin/ipfw del 001000 deny ip from 173.194.52.0/22 to any in

### Linux

	iptables -A OUTPUT -p tcp -d 173.194.52.0/22 -j REJECT --reject-with tcp-reset

### Proxy configuration

	function FindProxyForURL(url, host) {
		if (isInNet(host,"173.194.52.0","255.255.252.0") ) return "PROXY localhost:1";
		return "DIRECT";
	}

	function FindProxyForURL(url, host) {
		var hostRegex = /^r\d+---.*?\.c.youtube.com/;
		var urlRegex = /videoplayback\?/;
		if( hostRegex.test( host ) && !isInNet(host, "208.0.0.0", "255.0.0.0") && urlRegex.test( url ) ) 
			return "PROXY localhost:1";
		else
			return "DIRECT";
	}

#### Mac Configuration

Preferences > Network > each service > Advanced > Proxys > Automatique proxy configuration

URL: `file://localhost/.../file.pac`
