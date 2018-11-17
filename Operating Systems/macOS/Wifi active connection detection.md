## WiFi active connection

Aka captive portal

On iOS and OSX, when WiFi connection is detected, the OS try to open this URL: `http://captive.apple.com/hotspot-detect.html` (previously `http://apple.com/library/test/success.html`) which return `200 Ok` with content `<HTML><HEAD><TITLE>Success</TITLE></HEAD><BODY>Success</BODY></HTML>`

- https://stackoverflow.com/questions/18891706/ios7-and-captive-portals-changes-to-apple-request-url
- http://blog.erratasec.com/2010/09/apples-secret-wispr-request.html
- http://www.davidcalculli.com/blog/2012/10/apples-secret-connecting-to-a-wi-fi-network-requires-an-active-internet-connection
- [iOS Wi-Fi profiles: About Auto Join and per-connection password settings - Apple Support](https://support.apple.com/en-ca/HT202343)
- [How can I get Wifi if "http://www.apple.com/library/test/success.html" is blocked?](https://discussions.apple.com/message/19868615)
- https://en.wikipedia.org/wiki/Captive_portal
- `/System/Library/CoreServices called Captive Network Assistant.app` `/Library/Preferences/SystemConfiguration/CaptiveNetworkSupport/Settings.plist`
- http://apple.stackexchange.com/questions/211593/how-to-disable-captive-apple-com
- http://superuser.com/questions/937325/wifi-hotspot-why-os-does-not-detect-me-as-a-captive-portal
- http://blog.erratasec.com/2010/09/apples-secret-wispr-request.html

- http://www.dd-wrt.com/wiki/index.php/Chillispot
- http://coova.github.io/CoovaChilli/
- http://blog.trifork.com/2013/01/15/building-a-captive-portal-controlling-access-to-the-internet-from-your-network/
- https://www.howtoforge.com/tutorial/how-to-install-a-wireless-hotspot-with-captive-page-in-linux-using-coovachilli/
- https://learn.adafruit.com/setting-up-a-raspberry-pi-as-a-wifi-access-point/install-software
- http://www.pihomeserver.fr/2014/05/22/raspberry-pi-home-server-creer-hot-spot-wifi-captive-portal/
- http://www.pihomeserver.fr/2014/05/23/raspberry-pi-home-server-creer-hot-spot-wifi-portail-captif-22/